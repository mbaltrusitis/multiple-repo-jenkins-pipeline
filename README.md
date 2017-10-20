# multiple-repo-jenkins-pipeline

The objective is to have this `master` repo's Jenkinsfile checkout two other repositories without an error. In this example we are using Requests and Pelican. *Do not say to just use pip.* These are just example repositories I am using for this exercise.

The current state of `Jenkinsfile` produces the following behavior:

✅ Pipeline creates subdirectories for build deps.  
✅ Pipeline properly checks-out the root repo (this one)  
✅ Pipeline properly checks-out repo A (Python's Requests)  
❗️Pipeline fails to check-out repo B (Python’s Pelican)  

The error message for the second sibling repo makes it seem like its still referencing the first repo (Request's in this case):

```
Could not instantiate {source={GIT_AUTHOR_NAME=jenkins-bot, GIT_BRANCH=origin/master, GIT_COMMIT=db9da3e0d24c9902e801c45031beb3588d98b3e5, GIT_COMMITTER_NAME=jenkins-bot, GIT_LOCAL_BRANCH=master, GIT_URL=https://github.com/requests/requests.git}, targets=[master, master]} for ResolveScmStep(source: SCMSource{BitbucketSCMSource(repoOwner: String, repository: String, autoRegisterHook?(deprecated): boolean, bitbucketServerUrl?(deprecated): String, checkoutCredentialsId?(deprecated): String, credentialsId?: String, excludes?(deprecated): String, id?: String, includes?(deprecated): String, serverUrl?: String, traits?: SCMSourceTrait{AuthorInChangelogTrait() | CheckoutOptionTrait(extension: CheckoutOption(timeout: int)) | CleanAfterCheckoutTrait() | CleanBeforeCheckoutTrait() | CleanMercurialSCMSourceTrait() | CloneOptionTrait(extension: CloneOption(shallow: boolean, noTags: boolean, reference: String, timeout: int, depth?: int, honorRefspec?: boolean)) | GitBrowserSCMSourceTrait(browser: GitRepositoryBrowser{AssemblaWeb(repoUrl: String) | BitbucketWeb(repoUrl: String) | CGit(repoUrl: String) | FisheyeGitRepositoryBrowser(repoUrl: String) | GitBlitRepositoryBrowser(repoUrl: String, projectName: String) | GitLab(repoUrl: String, version: String) | GitList(repoUrl: String) | GitWeb(repoUrl: String) | GithubWeb(repoUrl: String) | Gitiles(repoUrl: String) | GitoriousWeb(repoUrl: String) | GogsGit(repoUrl: String) | KilnGit(repoUrl: String) | Phabricator(repoUrl: String, repo: String) | RedmineWeb(repoUrl: String) | RhodeCode(repoUrl: String) | Stash(repoUrl: String) | TFS2013GitRepositoryBrowser(repoUrl: String) | ViewGitWeb(repoUrl: String, projectName: String)}) | GitLFSPullTrait() | GitToolSCMSourceTrait(gitTool: String) | IgnoreOnPushNotificationTrait() | LocalBranchTrait() | MercurialBrowserSCMSourceTrait(browser: HgBrowser{BitBucket(url: String) | FishEye(url: String) | GoogleCode(url: String) | HgWeb(url: String) | Kallithea(url: String) | KilnHG(url: String) | RhodeCode(url: String) | RhodeCodeLegacy(url: String)}) | MercurialInstallationSCMSourceTrait(installation: String) | PruneStaleBranchTrait() | PublicRepoPullRequestFilterTrait() | RefSpecsSCMSourceTrait(templates: RefSpecTemplate(value: String)[]) | RegexSCMHeadFilterTrait(regex: String) | RemoteNameSCMSourceTrait(remoteName: String) | SubmoduleOptionTrait(extension: SubmoduleOption(disableSubmodules: boolean, recursiveSubmodules: boolean, trackingSubmodules: boolean, reference: String, timeout: int, parentCredentials: boolean)) | TagDiscoveryTrait() | UserIdentityTrait(extension: UserIdentity(name: String, email: String)) | WebhookRegistrationTrait(mode: String) | WildcardSCMHeadFilterTrait(includes: String, excludes: String) | WipeWorkspaceTrait() | com.cloudbees.jenkins.plugins.bitbucket.BranchDiscoveryTrait~BranchDiscoveryTrait(strategyId: int) | com.cloudbees.jenkins.plugins.bitbucket.ForkPullRequestDiscoveryTrait~ForkPullRequestDiscoveryTrait(strategyId: int, trust: java.lang.UnsupportedOperationException: do not know how to categorize attributes of type jenkins.scm.api.trait.SCMHeadAuthority<? super com.cloudbees.jenkins.plugins.bitbucket.BitbucketSCMSourceRequest, ? extends jenkins.scm.api.mixin.ChangeRequestSCMHead2, ? extends jenkins.scm.api.SCMRevision>) | com.cloudbees.jenkins.plugins.bitbucket.OriginPullRequestDiscoveryTrait~OriginPullRequestDiscoveryTrait(strategyId: int) | com.cloudbees.jenkins.plugins.bitbucket.SSHCheckoutTrait~SSHCheckoutTrait(credentialsId: String) | jenkins.plugins.git.traits.BranchDiscoveryTrait~BranchDiscoveryTrait() | org.jenkinsci.plugins.github_branch_source.BranchDiscoveryTrait~BranchDiscoveryTrait(strategyId: int) | org.jenkinsci.plugins.github_branch_source.ForkPullRequestDiscoveryTrait~ForkPullRequestDiscoveryTrait(strategyId: int, trust: java.lang.UnsupportedOperationException: do not know how to categorize attributes of type jenkins.scm.api.trait.SCMHeadAuthority<? super org.jenkinsci.plugins.github_branch_source.GitHubSCMSourceRequest, ? extends jenkins.scm.api.mixin.ChangeRequestSCMHead2, ? extends jenkins.scm.api.SCMRevision>) | org.jenkinsci.plugins.github_branch_source.OriginPullRequestDiscoveryTrait~OriginPullRequestDiscoveryTrait(strategyId: int) | org.jenkinsci.plugins.github_branch_source.SSHCheckoutTrait~SSHCheckoutTrait(credentialsId: String)}[]) | GitHubSCMSource(repoOwner: String, repository: String, apiUri?: String, buildForkPRHead?(deprecated): boolean, buildForkPRMerge?(deprecated): boolean, buildOriginBranch?(deprecated): boolean, buildOriginBranchWithPR?(deprecated): boolean, buildOriginPRHead?(deprecated): boolean, buildOriginPRMerge?(deprecated): boolean, credentialsId?: String, excludes?(deprecated): String, id?: String, includes?(deprecated): String, traits?: SCMSourceTrait{AuthorInChangelogTrait() | CheckoutOptionTrait(extension: CheckoutOption(timeout: int)) | CleanAfterCheckoutTrait() | CleanBeforeCheckoutTrait() | CleanMercurialSCMSourceTrait() | CloneOptionTrait(extension: CloneOption(shallow: boolean, noTags: boolean, reference: String, timeout: int, depth?: int, honorRefspec?: boolean)) | GitBrowserSCMSourceTrait(browser: GitRepositoryBrowser{AssemblaWeb(repoUrl: String) | BitbucketWeb(repoUrl: String) | CGit(repoUrl: String) | FisheyeGitRepositoryBrowser(repoUrl: String) | GitBlitRepositoryBrowser(repoUrl: String, projectName: String) | GitLab(repoUrl: String, version: String) | GitList(repoUrl: String) | GitWeb(repoUrl: String) | GithubWeb(repoUrl: String) | Gitiles(repoUrl: String) | GitoriousWeb(repoUrl: String) | GogsGit(repoUrl: String) | KilnGit(repoUrl: String) | Phabricator(repoUrl: String, repo: String) | RedmineWeb(repoUrl: String) | RhodeCode(repoUrl: String) | Stash(repoUrl: String) | TFS2013GitRepositoryBrowser(repoUrl: String) | ViewGitWeb(repoUrl: String, projectName: String)}) | GitLFSPullTrait() | GitToolSCMSourceTrait(gitTool: String) | IgnoreOnPushNotificationTrait() | LocalBranchTrait() | MercurialBrowserSCMSourceTrait(browser: HgBrowser{BitBucket(url: String) | FishEye(url: String) | GoogleCode(url: String) | HgWeb(url: String) | Kallithea(url: String) | KilnHG(url: String) | RhodeCode(url: String) | RhodeCodeLegacy(url: String)}) | MercurialInstallationSCMSourceTrait(installation: String) | PruneStaleBranchTrait() | PublicRepoPullRequestFilterTrait() | RefSpecsSCMSourceTrait(templates: RefSpecTemplate(value: String)[]) | RegexSCMHeadFilterTrait(regex: String) | RemoteNameSCMSourceTrait(remoteName: String) | SubmoduleOptionTrait(extension: SubmoduleOption(disableSubmodules: boolean, recursiveSubmodules: boolean, trackingSubmodules: boolean, reference: String, timeout: int, parentCredentials: boolean)) | TagDiscoveryTrait() | UserIdentityTrait(extension: UserIdentity(name: String, email: String)) | WebhookRegistrationTrait(mode: String) | WildcardSCMHeadFilterTrait(includes: String, excludes: String) | WipeWorkspaceTrait() | com.cloudbees.jenkins.plugins.bitbucket.BranchDiscoveryTrait~BranchDiscoveryTrait(strategyId: int) | com.cloudbees.jenkins.plugins.bitbucket.ForkPullRequestDiscoveryTrait~ForkPullRequestDiscoveryTrait(strategyId: int, trust: java.lang.UnsupportedOperationException: do not know how to categorize attributes of type jenkins.scm.api.trait.SCMHeadAuthority<? super com.cloudbees.jenkins.plugins.bitbucket.BitbucketSCMSourceRequest, ? extends jenkins.scm.api.mixin.ChangeRequestSCMHead2, ? extends jenkins.scm.api.SCMRevision>) | com.cloudbees.jenkins.plugins.bitbucket.OriginPullRequestDiscoveryTrait~OriginPullRequestDiscoveryTrait(strategyId: int) | com.cloudbees.jenkins.plugins.bitbucket.SSHCheckoutTrait~SSHCheckoutTrait(credentialsId: String) | jenkins.plugins.git.traits.BranchDiscoveryTrait~BranchDiscoveryTrait() | org.jenkinsci.plugins.github_branch_source.BranchDiscoveryTrait~BranchDiscoveryTrait(strategyId: int) | org.jenkinsci.plugins.github_branch_source.ForkPullRequestDiscoveryTrait~ForkPullRequestDiscoveryTrait(strategyId: int, trust: java.lang.UnsupportedOperationException: do not know how to categorize attributes of type jenkins.scm.api.trait.SCMHeadAuthority<? super org.jenkinsci.plugins.github_branch_source.GitHubSCMSourceRequest, ? extends jenkins.scm.api.mixin.ChangeRequestSCMHead2, ? extends jenkins.scm.api.SCMRevision>) | org.jenkinsci.plugins.github_branch_source.OriginPullRequestDiscoveryTrait~OriginPullRequestDiscoveryTrait(strategyId: int) | org.jenkinsci.plugins.github_branch_source.SSHCheckoutTrait~SSHCheckoutTrait(credentialsId: String)}[]) | GitSCMSource(remote: String, browser?: GitRepositoryBrowser{AssemblaWeb(repoUrl: String) | BitbucketWeb(repoUrl: String) | CGit(repoUrl: String) | FisheyeGitRepositoryBrowser(repoUrl: String) | GitBlitRepositoryBrowser(repoUrl: String, projectName: String) | GitLab(repoUrl: String, version: String) | GitList(repoUrl: String) | GitWeb(repoUrl: String) | GithubWeb(repoUrl: String) | Gitiles(repoUrl: String) | GitoriousWeb(repoUrl: String) | GogsGit(repoUrl: String) | KilnGit(repoUrl: String) | Phabricator(repoUrl: String, repo: String) | RedmineWeb(repoUrl: String) | RhodeCode(repoUrl: String) | Stash(repoUrl: String) | TFS2013GitRepositoryBrowser(repoUrl: String) | ViewGitWeb(repoUrl: String, projectName: String)}, credentialsId?: String, extensions?(deprecated): GitSCMExtension{AuthorInChangelog() | BuildChooserSetting(buildChooser: BuildChooser{AncestryBuildChooser(maximumAgeInDays: int, ancestorCommitSha1: String) | DefaultBuildChooser() | InverseBuildChooser()}) | ChangelogToBranch(options: ChangelogToBranchOptions(compareRemote: String, compareTarget: String)) | CheckoutOption(timeout: int) | CleanBeforeCheckout() | CleanCheckout() | CloneOption(shallow: boolean, noTags: boolean, reference: String, timeout: int, depth?: int, honorRefspec?: boolean) | DisableRemotePoll() | GitLFSPull() | IgnoreNotifyCommit() | LocalBranch(localBranch: String) | MessageExclusion(excludedMessage: String) | PathRestriction(includedRegions: String, excludedRegions: String) | PerBuildTag() | PreBuildMerge(options: UserMergeOptions(mergeRemote: String, mergeTarget: String, mergeStrategy: String, fastForwardMode: GitPluginFastForwardMode[FF, FF_ONLY, NO_FF])) | PruneStaleBranch() | RelativeTargetDirectory(relativeTargetDir: String) | ScmName(name: String) | SparseCheckoutPaths(sparseCheckoutPaths: SparseCheckoutPath(path: String)[]) | SubmoduleOption(disableSubmodules: boolean, recursiveSubmodules: boolean, trackingSubmodules: boolean, reference: String, timeout: int, parentCredentials: boolean) | UserExclusion(excludedUsers: String) | UserIdentity(name: String, email: String) | WipeWorkspace()}[], gitTool?: String, id?: String, traits?: SCMSourceTrait{AuthorInChangelogTrait() | CheckoutOptionTrait(extension: CheckoutOption(timeout: int)) | CleanAfterCheckoutTrait() | CleanBeforeCheckoutTrait() | CleanMercurialSCMSourceTrait() | CloneOptionTrait(extension: CloneOption(shallow: boolean, noTags: boolean, reference: String, timeout: int, depth?: int, honorRefspec?: boolean)) | GitBrowserSCMSourceTrait(browser: GitRepositoryBrowser{AssemblaWeb(repoUrl: String) | BitbucketWeb(repoUrl: String) | CGit(repoUrl: String) | FisheyeGitRepositoryBrowser(repoUrl: String) | GitBlitRepositoryBrowser(repoUrl: String, projectName: String) | GitLab(repoUrl: String, version: String) | GitList(repoUrl: String) | GitWeb(repoUrl: String) | GithubWeb(repoUrl: String) | Gitiles(repoUrl: String) | GitoriousWeb(repoUrl: String) | GogsGit(repoUrl: String) | KilnGit(repoUrl: String) | Phabricator(repoUrl: String, repo: String) | RedmineWeb(repoUrl: String) | RhodeCode(repoUrl: String) | Stash(repoUrl: String) | TFS2013GitRepositoryBrowser(repoUrl: String) | ViewGitWeb(repoUrl: String, projectName: String)}) | GitLFSPullTrait() | GitToolSCMSourceTrait(gitTool: String) | IgnoreOnPushNotificationTrait() | LocalBranchTrait() | MercurialBrowserSCMSourceTrait(browser: HgBrowser{BitBucket(url: String) | FishEye(url: String) | GoogleCode(url: String) | HgWeb(url: String) | Kallithea(url: String) | KilnHG(url: String) | RhodeCode(url: String) | RhodeCodeLegacy(url: String)}) | MercurialInstallationSCMSourceTrait(installation: String) | PruneStaleBranchTrait() | PublicRepoPullRequestFilterTrait() | RefSpecsSCMSourceTrait(templates: RefSpecTemplate(value: String)[]) | RegexSCMHeadFilterTrait(regex: String) | RemoteNameSCMSourceTrait(remoteName: String) | SubmoduleOptionTrait(extension: SubmoduleOption(disableSubmodules: boolean, recursiveSubmodules: boolean, trackingSubmodules: boolean, reference: String, timeout: int, parentCredentials: boolean)) | TagDiscoveryTrait() | UserIdentityTrait(extension: UserIdentity(name: String, email: String)) | WebhookRegistrationTrait(mode: String) | WildcardSCMHeadFilterTrait(includes: String, excludes: String) | WipeWorkspaceTrait() | com.cloudbees.jenkins.plugins.bitbucket.BranchDiscoveryTrait~BranchDiscoveryTrait(strategyId: int) | com.cloudbees.jenkins.plugins.bitbucket.ForkPullRequestDiscoveryTrait~ForkPullRequestDiscoveryTrait(strategyId: int, trust: java.lang.UnsupportedOperationException: do not know how to categorize attributes of type jenkins.scm.api.trait.SCMHeadAuthority<? super com.cloudbees.jenkins.plugins.bitbucket.BitbucketSCMSourceRequest, ? extends jenkins.scm.api.mixin.ChangeRequestSCMHead2, ? extends jenkins.scm.api.SCMRevision>) | com.cloudbees.jenkins.plugins.bitbucket.OriginPullRequestDiscoveryTrait~OriginPullRequestDiscoveryTrait(strategyId: int) | com.cloudbees.jenkins.plugins.bitbucket.SSHCheckoutTrait~SSHCheckoutTrait(credentialsId: String) | jenkins.plugins.git.traits.BranchDiscoveryTrait~BranchDiscoveryTrait() | org.jenkinsci.plugins.github_branch_source.BranchDiscoveryTrait~BranchDiscoveryTrait(strategyId: int) | org.jenkinsci.plugins.github_branch_source.ForkPullRequestDiscoveryTrait~ForkPullRequestDiscoveryTrait(strategyId: int, trust: java.lang.UnsupportedOperationException: do not know how to categorize attributes of type jenkins.scm.api.trait.SCMHeadAuthority<? super org.jenkinsci.plugins.github_branch_source.GitHubSCMSourceRequest, ? extends jenkins.scm.api.mixin.ChangeRequestSCMHead2, ? extends jenkins.scm.api.SCMRevision>) | org.jenkinsci.plugins.github_branch_source.OriginPullRequestDiscoveryTrait~OriginPullRequestDiscoveryTrait(strategyId: int) | org.jenkinsci.plugins.github_branch_source.SSHCheckoutTrait~SSHCheckoutTrait(credentialsId: String)}[]) | MercurialSCMSource(source: String, credentialsId?: String, id?: String, traits?: java.lang.UnsupportedOperationException: do not know how to categorize attributes of type ? extends jenkins.scm.api.trait.SCMSourceTrait[]) | SingleSCMSource(name: String, scm: SCM{GitSCM(userRemoteConfigs: UserRemoteConfig(url: String, name: String, refspec: String, credentialsId: String)[], branches: BranchSpec(name: String)[], doGenerateSubmoduleConfigurations: boolean, submoduleCfg: org.kohsuke.stapler.NoStaplerConstructorException: There's no @DataBoundConstructor on any constructor of class hudson.plugins.git.SubmoduleConfig[], browser: GitRepositoryBrowser{AssemblaWeb(repoUrl: String) | BitbucketWeb(repoUrl: String) | CGit(repoUrl: String) | FisheyeGitRepositoryBrowser(repoUrl: String) | GitBlitRepositoryBrowser(repoUrl: String, projectName: String) | GitLab(repoUrl: String, version: String) | GitList(repoUrl: String) | GitWeb(repoUrl: String) | GithubWeb(repoUrl: String) | Gitiles(repoUrl: String) | GitoriousWeb(repoUrl: String) | GogsGit(repoUrl: String) | KilnGit(repoUrl: String) | Phabricator(repoUrl: String, repo: String) | RedmineWeb(repoUrl: String) | RhodeCode(repoUrl: String) | Stash(repoUrl: String) | TFS2013GitRepositoryBrowser(repoUrl: String) | ViewGitWeb(repoUrl: String, projectName: String)}, gitTool: String, extensions: GitSCMExtension{AuthorInChangelog() | BuildChooserSetting(buildChooser: BuildChooser{AncestryBuildChooser(maximumAgeInDays: int, ancestorCommitSha1: String) | DefaultBuildChooser() | InverseBuildChooser()}) | ChangelogToBranch(options: ChangelogToBranchOptions(compareRemote: String, compareTarget: String)) | CheckoutOption(timeout: int) | CleanBeforeCheckout() | CleanCheckout() | CloneOption(shallow: boolean, noTags: boolean, reference: String, timeout: int, depth?: int, honorRefspec?: boolean) | DisableRemotePoll() | GitLFSPull() | IgnoreNotifyCommit() | LocalBranch(localBranch: String) | MessageExclusion(excludedMessage: String) | PathRestriction(includedRegions: String, excludedRegions: String) | PerBuildTag() | PreBuildMerge(options: UserMergeOptions(mergeRemote: String, mergeTarget: String, mergeStrategy: String, fastForwardMode: GitPluginFastForwardMode[FF, FF_ONLY, NO_FF])) | PruneStaleBranch() | RelativeTargetDirectory(relativeTargetDir: String) | ScmName(name: String) | SparseCheckoutPaths(sparseCheckoutPaths: SparseCheckoutPath(path: String)[]) | SubmoduleOption(disableSubmodules: boolean, recursiveSubmodules: boolean, trackingSubmodules: boolean, reference: String, timeout: int, parentCredentials: boolean) | UserExclusion(excludedUsers: String) | UserIdentity(name: String, email: String) | WipeWorkspace()}[]) | MercurialSCM(source: String, browser?: HgBrowser{BitBucket(url: String) | FishEye(url: String) | GoogleCode(url: String) | HgWeb(url: String) | Kallithea(url: String) | KilnHG(url: String) | RhodeCode(url: String) | RhodeCodeLegacy(url: String)}, clean?: boolean, credentialsId?: String, disableChangeLog?: boolean, installation?: String, modules?: String, revision?: String, revisionType?: RevisionType[BRANCH, TAG, CHANGESET, REVSET], subdir?: String) | NullSCM() | SubversionSCM(locations: ModuleLocation(remote: String, credentialsId: String, local: String, depthOption: String, ignoreExternalsOption: boolean)[], workspaceUpdater: WorkspaceUpdater{CheckoutUpdater() | NoopUpdater() | UpdateUpdater() | UpdateWithCleanUpdater() | UpdateWithRevertUpdater()}, browser: SubversionRepositoryBrowser{Assembla(spaceName: String) | CollabNetSVN(url: String) | FishEyeSVN(url: String, rootModule: String) | Phabricator(url: String, repo: String) | SVNWeb(url: String) | Sventon(url: String, repositoryInstance: String) | Sventon2(url: String, repositoryInstance: String) | ViewSVN(url: String) | WebSVN(url: String)}, excludedRegions: String, excludedUsers: String, excludedRevprop: String, excludedCommitMessages: String, includedRegions: String, ignoreDirPropChanges: boolean, filterChangelog: boolean, additionalCredentials: AdditionalCredentials(realm: String, credentialsId: String)[])}, id?: String) | SubversionSCMSource(id?: String, remoteBase: String, credentialsId?: String, excludes?: String, includes?: String)}, targets: String[], ignoreErrors?: boolean): java.lang.UnsupportedOperationException: must specify $class with an implementation of class jenkins.scm.api.SCMSource
```
