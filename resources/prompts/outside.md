Can you generate a JSON schema which follows the specification of draft-7 from the struct type in golang?
If it's impossible to create a complete JSON schema, please tell me missing definitions.

type OrgOptConfig struct {
	// OptOutStrategy : set to true to change from opt-in to opt-out.
	OptOutStrategy bool `json:"optOutStrategy"`

	// OptInRepos is the list of repos to opt-in when in opt-in strategy.
	OptInRepos []string `json:"optInRepos"`

	// OptOutRepos is the list of repos to opt-out when in opt-out strategy.
	OptOutRepos []string `json:"optOutRepos"`

	// OptOutPrivateRepos : set to true to not access private repos.
	OptOutPrivateRepos bool `json:"optOutPrivateRepos"`

	// OptOutPublicRepos : set to true to not access public repos.
	OptOutPublicRepos bool `json:"optOutPublicRepos"`

	// OptOutArchivedRepos : set to true to opt-out archived repositories.
	OptOutArchivedRepos bool `json:"optOutArchivedRepos"`

	// OptOutForkedRepos : set to true to opt-out forked repositories.
	OptOutForkedRepos bool `json:"optOutForkedRepos"`

	// DisableRepoOverride : set to true to disallow repos from opt-in/out in
	// their config.
	DisableRepoOverride bool `json:"disableRepoOverride"`
}

type OutsideExemption struct {
	// User is a GitHub username
	User string `json:"user"`

	// Repo is a GitHub repo name
	Repo string `json:"repo"`

	// Push allows push permission
	Push bool `json:"push"`

	// Admin allows admin permission
	Admin bool `json:"admin"`
}

type OrgConfig struct {
	// OptConfig is the standard org-level opt in/out config, RepoOverride
	// applies to all config.
	OptConfig config.OrgOptConfig `json:"optConfig"`

	// Action defines which action to take, default log, other: issue...
	Action string `json:"action"`

	// PushAllowed defined if outside collaborators are allowed to have push
	// access, default true.
	PushAllowed bool `json:"pushAllowed"`

	// AdminAllowed defined if outside collaborators are allowed to have admin
	// access, default false.
	AdminAllowed bool `json:"adminAllowed"`

	// Exemptions is a list of user-repo-access pairings to exempt.
	// Exemptions are only defined at the org level because they should be made
	// obvious to org security managers.
	Exemptions []*OutsideExemption `json:"exemptions"`
}
