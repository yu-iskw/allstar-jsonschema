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

type AdministratorExemption struct {

	// Repo is a GitHub repo name. Globs are allowed.
	Repo string `json:"repo"`

	// OwnerlessAllowed defines if repositories are allowed to have no
	// administrators, default false.
	OwnerlessAllowed bool `json:"ownerlessAllowed"`

	// Whether to allow users to be admins on a repo. If false then only teams can be admins. Default true.
	UserAdminsAllowed bool `json:"userAdminsAllowed"`

	// Allow specific users to be admins on this repository. It overrides the boolean value UserAdminsAllowed.
	UserAdmins []string `json:"userAdmins"`

	// The maximum number of users with admin permissions on this repo that are allowed.  It overrides the int value MaxNumberUserAdmins.
	// It only takes effect if a value > 0 is specified. If you wish to disallow user admins in general, please use the userAdminsAllowed bool instead.
	MaxNumberUserAdmins int `json:"maxNumberUserAdmins"`

	// Whether to allow teams to be admins on a repo. If false then only users can be admins. Default true.
	TeamAdminsAllowed bool `json:"teamAdminsAllowed"`

	// Allow specific teams to be admins on this repository. It overrides the boolean value TeamAdminsAllowed.
	TeamAdmins []string `json:"teamAdmins"`

	// The maximum number of teams with admin permissions on this repo that are allowed. It overrides the int value MaxNumberAdminTeams.
	// It only takes effect if a value > 0 is specified. If you wish to disallow admin teams in general, please use the teamAdminsAllowed bool instead.
	MaxNumberAdminTeams int `json:"maxNumberAdminTeams"`
}

type OrgConfig struct {
	// OptConfig is the standard org-level opt in/out config, RepoOverride
	// applies to all config.
	OptConfig config.OrgOptConfig `json:"optConfig"`

	// Action defines which action to take, default log, other: issue...
	Action string `json:"action"`

	// OwnerlessAllowed defines if repositories are allowed to have no
	// administrators, default false.
	OwnerlessAllowed bool `json:"ownerlessAllowed"`

	// Whether to allow users to be admins on a repo. If false then only teams can be admins. Default true.
	UserAdminsAllowed bool `json:"userAdminsAllowed"`

	// The maximum number of users with admin permissions on a repo that are allowed.
	// It only takes effect if a value > 0 is specified. If you wish to disallow user admins in general, please use the userAdminsAllowed bool instead.
	MaxNumberUserAdmins int `json:"maxNumberUserAdmins"`

	// Whether to allow teams to be admins on a repo. If false then only users can be admins. Default true.
	TeamAdminsAllowed bool `json:"teamAdminsAllowed"`

	// The maximum number of teams with admin permissions on a repo that are allowed.
	// It only takes effect if a value > 0 is specified. If you wish to disallow admin teams in general, please use the teamAdminsAllowed bool instead.
	MaxNumberAdminTeams int `json:"maxNumberAdminTeams"`

	// Exemptions is a list of repo-bool pairings to exempt.
	// Exemptions are only defined at the org level because they should be made
	// obvious to org security managers.
	Exemptions []*AdministratorExemption `json:"exemptions"`
}
