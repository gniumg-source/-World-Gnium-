Eligible repositories for CodeQL default setup at scale
A repository must meet all the following criteria to be eligible for default setup, otherwise you need to use advanced setup.

Advanced setup for code scanning is not already enabled.
GitHub Actions are enabled.
It is publicly visible, or GitHub Code Security is enabled.
We recommend enabling default setup for eligible repositories if there is any chance the repositories will include at least one CodeQL-supported language in the future. If you enable default setup on a repository that does not include any CodeQL-supported languages, default setup will not run any scans or use any GitHub Actions minutes. If CodeQL-supported languages are added to the repository's default branch, default setup will automatically begin scanning CodeQL-supported languages and using GitHub Actions minutes. For more information on CodeQL-supported languages, see About code scanning with CodeQL.

About adding languages to an existing default setup configuration
If the code in a repository changes to include a CodeQL-supported language, GitHub will automatically update the code scanning configuration to include the new language. If code scanning fails with the new configuration, GitHub will resume the previous configuration automatically so the repository does not lose code scanning coverage.

Providing default setup access to private registries
When a repository uses code stored in a private registry, default setup needs access to the registry to work effectively. For more information, see Giving security features access to private registries.

Configuring default setup for all eligible repositories in an organization
You can enable default setup for all eligible repositories in your organization. For more information, see About enabling security features at scale.

Extending CodeQL coverage in default setup
Through your organization's security settings page, you can extend coverage in default setup using model packs for all eligible repositories in your organization. For more information, see Editing your configuration of default setup.

Configuring default setup for a subset of repositories in an organization
You can filter for specific repositories you would like to configure default setup for. For more information, see Applying a custom security configuration.
