Can you generate a JSON schema which follows the specification of draft-7 from the struct type in golang?
If it's impossible to create a complete JSON schema, please tell me missing definitions.

type RepoOptConfig struct {
	// OptIn : set to true to opt-in this repo when in opt-in strategy
	OptIn bool `json:"optIn"`

	// OptOut: set to true to opt-out this repo when in opt-out strategy
	OptOut bool `json:"optOut"`
}

type ScheduleConfig struct {
	// Timezone specifies a timezone, eg. "America/Los_Angeles"
	// See https://en.wikipedia.org/wiki/List_of_tz_database_time_zones#List
	Timezone string `json:"timezone"`

	// Days specifies up to three weekdays during which to disable pings.
	// eg. "saturday" or "sunday"
	Days []string `json:"days"`
}

type RepoConfig struct {
	// OptConfig contains the opt in/out configuration.
	OptConfig RepoOptConfig `json:"optConfig"`

	// IssueLabel is the label used to tag, search, and identify GitHub Issues
	// created by the bot. Repo-level label my override Org-level setting
	// regardless of Optconfig.DisableRepoOverride.
	IssueLabel string `json:"issueLabel"`

	// Schedule specifies days during which to not send notifications,
	Schedule *ScheduleConfig `json:"schedule"`
}
