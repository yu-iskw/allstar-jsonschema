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
	// OptConfig is the standard org-level opt in/out config, RepoOverride
	// applies to all config.
	OptConfig config.OrgOptConfig `json:"optConfig"`

	// Action defines which action to take, default log, other: issue...
	Action string `json:"action"`

	// Checks is a list of check names to run from Security Scorecards. These
	// must match the name that the check uses in it's call to
	// "registerCheck". See the check code for each name:
	// https://github.com/ossf/scorecard/tree/main/checks For example, the name
	// for the Signed Releases check is "Signed-Releases".
	Checks []string `json:"checks"`

	// Threshold is the score threshold that checks must meet to pass the
	// policy. If all checks score equal or above the threshold, the Allstar
	// policy will pass. The default is checker.MaxResultScore:
	// https://pkg.go.dev/github.com/ossf/scorecard/v4@v4.4.0/checker#pkg-constants
	Threshold int `json:"threshold"`
}
