Can you generate a JSON schema which follows the specification of draft-7 from the struct type in golang?
If it's impossible to create a complete JSON schema, please tell me missing definitions.

type RepoSelector struct {
	// Name is the repo name in glob format
	Name string `json:"name"`

	// Language is a set of programming languages.
	// See the section about language detection below
	Language []string `json:"language"`

	// Exclude is a set of RepoSelectors targeting repos that should
	// not be matched by this selector.
	Exclude []*RepoSelector `json:"exclude"`
}

type ActionSelector struct {
	// Name is the Action name in glob format
	Name string `json:"name"`

	// Version is a semver condition or commit ref
	// Default "" targets any version
	Version string `json:"version"`
}

type Rule struct {
	// Name is the name used to identify the rule
	Name string `json:"name"`

	// Method is the type of rule. One of "require", "allow", and "deny".
	Method string `json:"method"`

	// Priority is the priority tier identifier applied to the rule.
	// Options are "urgent", "high", "medium", and "low"
	Priority string `json:"priority"`

	// Actions is a set of ActionSelectors.
	// If nil, all Actions will be selected
	Actions []*ActionSelector `json:"actions"`

	// MustPass specifies whether the rule's Action(s) are required to
	// be part of a passing workflow on latest commit.
	// [For use with "require" method]
	MustPass bool `json:"mustPass"`

	// RequireAll specifies that all Actions listed should be required,
	// rather than just one.
	// [For use with "require" method]
	RequireAll bool `json:"requireAll"`
}

type RuleGroup struct {
	// Name is the name used to identify the RuleGroup.
	Name string `json:"name"`

	// Repos is the set of RepoSelectors to use when deciding whether a repo
	// qualifies for this RuleGroup.
	// if nil, select all repos.
	Repos []*RepoSelector `json:"repos"`

	// Rules is the set of rules to apply for this RuleGroup.
	// Rules are applied in order of priority, with allow/require rules
	// evaluated before deny rules at each priority tier.
	Rules []*Rule `json:"rules"`
}

type OrgConfig struct {
	// Action defines which action to take, default log, other: issue...
	Action string `json:"action"`

	// Groups is the set of RuleGroups to employ during Check.
	// They are evaluated in order.
	Groups []*RuleGroup `json:"groups"`
}
