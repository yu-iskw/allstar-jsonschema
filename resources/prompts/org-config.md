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

type ScheduleConfig struct {
	// Timezone specifies a timezone, eg. "America/Los_Angeles"
	// See https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List
	Timezone string `json:"timezone"`

	// Days specifies up to three weekdays during which to disable pings.
	// eg. "saturday" or "sunday"
	Days []string `json:"days"`
}

type OrgConfig struct {
	// OptConfig contains the opt in/out configuration.
	OptConfig OrgOptConfig `json:"optConfig"`

	// IssueLabel is the label used to tag, search, and identify GitHub Issues
	// created by the bot. The default is specified by the operator of Allstar,
	// currently: "allstar"
	IssueLabel string `json:"issueLabel"`

	// IssueRepo is the name of a repository in the organization to create issues
	// in. If left unset, by default Allstar will create issues in the repository
	// that is out of compliance. Setting the IssueRepo will instruct Allstar to
	// only create issues in the specified repository for non-compliance found in
	// any repository in the organization.
	//
	// This can be useful for previewing the issues that Allstar would create in
	// all repositories. Also, it can be used to centrally audit non-compliance
	// issues.
	//
	// Note: When changing this setting, Allstar does not clean up previously
	// created issues from a previous setting.
	IssueRepo string `json:"issueRepo"`

	// IssueFooter is a custom message to add to the end of all Allstar created
	// issues in the GitHub organization. It does not supercede the bot-level
	// footer (found in pkg/config/operator) but is added in addition to that
	// one. This setting is useful to direct users to the organization-level
	// config repository or documentation describing your Allstar settings and
	// policies.
	IssueFooter string `json:"issueFooter"`

	// Schedule specifies whether to perform certain actions on specific days.
	Schedule *ScheduleConfig `json:"schedule"`
}
