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

type OrgConfig struct {
	// OptConfig is the standard org-level opt in/out config, RepoOverride applies to all
	// config.
	OptConfig config.OrgOptConfig `json:"optConfig"`

	// Action defines which action to take, default log, other: issue...
	Action string `json:"action"`

	// IgnoreFiles is a list of file names to ignore. Any Binary Artifacts found
	// with these names are allowed, and the policy may still pass. These are
	// just the file name, not a full path. Globs are not allowed.
	IgnoreFiles []string `json:"ignoreFiles"`
}

type RepoOptConfig struct {
	// OptIn : set to true to opt-in this repo when in opt-in strategy
	OptIn bool `json:"optIn"`

	// OptOut: set to true to opt-out this repo when in opt-out strategy
	OptOut bool `json:"optOut"`
}

type RepoConfig struct {
	// OptConfig is the standard repo-level opt in/out config.
	OptConfig config.RepoOptConfig `json:"optConfig"`

	// Action overrides the same setting in org-level, only if present.
	Action *string `json:"action"`

	// IgnorePaths is a list of full paths to ignore. If these are reported as a
	// Binary Artifact, they will be ignored and the policy may still pass. These
	// must be full paths with directories. Globs are not allowed. These are
	// allowed even if RepoOverride is false.
	IgnorePaths []string `json:"ignorePaths"`
}
