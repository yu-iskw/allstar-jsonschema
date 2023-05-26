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

type RepoOptConfig struct {
	// OptIn : set to true to opt-in this repo when in opt-in strategy
	OptIn bool `json:"optIn"`

	// OptOut: set to true to opt-out this repo when in opt-out strategy
	OptOut bool `json:"optOut"`
}

type OrgConfig struct {
	// OptConfig is the standard org-level opt in/out config, RepoOverride
	// applies to all BP config.
	OptConfig config.OrgOptConfig `json:"optConfig"`

	// Action defines which action to take, default log, other: issue...
	Action string `json:"action"`

	// EnforceDefault : set to true to enforce policy on default branch, default
	// true.
	EnforceDefault bool `json:"enforceDefault"`

	// EnforceBranches is a map of repos and branches. These are other
	// non-default branches to enforce policy on, such as branches which releases
	// are made from.
	EnforceBranches map[string][]string `json:"enforceBranches"`

	// RequireApproval : set to true to enforce approval on PRs, default true.
	RequireApproval bool `json:"requireApproval"`

	// RequireCodeOwnerReviews : set to true to enforce code owner reviews on PRs, default false.
	// If set to true, then "requireApproval" must also be true
	RequireCodeOwnerReviews bool `json:"requireCodeOwnerReviews"`

	// ApprovalCount is the number of required PR approvals, default 1.
	ApprovalCount int `json:"approvalCount"`

	// DismissStale : set to true to require PR approvals be dismissed when a PR
	// is updated, default true.
	DismissStale bool `json:"dismissStale"`

	// BlockForce : set to true to block force pushes, default true.
	BlockForce bool `json:"blockForce"`

	// RequireUpToDateBranch : set to true to require that branches must be up
	// to date before merging. Only used if RequireStatusChecks is set. Default
	// true.
	RequireUpToDateBranch bool `json:"requireUpToDateBranch"`

	// RequireStatusChecks is a list of status checks that are required in
	// order to merge into the protected branch. Each entry must specify
	// the context, and optionally an appID.
	RequireStatusChecks []StatusCheck `json:"requireStatusChecks"`

	// EnforceOnAdmins : set to true to apply the branch protection rules on
	// administrators as well.
	EnforceOnAdmins bool `json:"enforceOnAdmins"`

	// RequireSignedCommits : set to true to require signed commits on protected branches, default false
	RequireSignedCommits bool `json:"requireSignedCommits"`
}

type StatusCheck struct {
	// Context is the status check name that should be required.
	Context string `json:"context"`

	// AppID, when provided, will require that the status check be set by
	// the GitHub App with the given AppID. When omitted, any app can
	// provide the required status check.
	AppID *int64 `json:"appID"`
}
