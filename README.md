# gitversion-issue-2967-reproduction

## Link

https://github.com/GitTools/GitVersion/issues/2967

## How to reproduce problem?

1. Clone repository
2. Switch to `issue-branch` branch.
3. execute `dotnet-gitversion` in repository.
4. Issue:
```powershell
INFO [01/19/22 20:27:57:46] End: Attempting to inherit branch configuration from parent branch (Took: 29.70ms)
  ERROR [01/19/22 20:27:57:51] An unexpected error occurred:
System.NullReferenceException: Object reference not set to an instance of an object.
   at GitVersion.GitObject..ctor(GitObject innerGitObject) in D:\a\GitVersion\GitVersion\src\GitVersion.LibGit2Sharp\Git\GitObject.cs:line 12
   at GitVersion.Commit..ctor(Commit innerCommit) in D:\a\GitVersion\GitVersion\src\GitVersion.LibGit2Sharp\Git\Commit.cs:line 12
   at GitVersion.GitRepository.<>c__DisplayClass27_0.<FindMergeBase>b__0() in D:\a\GitVersion\GitVersion\src\GitVersion.LibGit2Sharp\Git\GitRepository.cs:line 61
   at Polly.Policy`1.<>c__DisplayClass11_0.<Execute>b__0(Context ctx, CancellationToken ct)
   at Polly.Retry.RetryEngine.Implementation[TResult](Func`3 action, Context context, CancellationToken cancellationToken, ExceptionPredicates shouldRetryExceptionPredicates, ResultPredicates`1 shouldRetryResultPredicates, Action`4 onRetry, Int32 permittedRetryCount, IEnumerable`1 sleepDurationsEnumerable, Func`4 sleepDurationProvider)
   at Polly.Retry.RetryPolicy`1.Implementation(Func`3 action, Context context, CancellationToken cancellationToken)
   at Polly.Policy`1.Execute(Func`3 action, Context context, CancellationToken cancellationToken)
   at Polly.Policy`1.Execute(Func`1 action)
   at GitVersion.Helpers.RetryAction`2.Execute(Func`1 operation) in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Helpers\RetryAction.cs:line 35
   at GitVersion.GitRepository.FindMergeBase(ICommit commit, ICommit otherCommit) in D:\a\GitVersion\GitVersion\src\GitVersion.LibGit2Sharp\Git\GitRepository.cs:line 59
   at GitVersion.RepositoryStore.FindMergeBase(IBranch branch, IBranch otherBranch) in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Core\RepositoryStore.cs:line 49
   at GitVersion.RepositoryStore.<>c__DisplayClass30_0.<GetMergeCommitsForBranch>b__2(IBranch otherBranch) in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Core\RepositoryStore.cs:line 454
   at System.Linq.Enumerable.WhereSelectEnumerableIterator`2.MoveNext()
   at System.Linq.Enumerable.WhereEnumerableIterator`1.ToArray()
   at System.Linq.OrderedEnumerable`1.ToList()
   at System.Linq.Enumerable.ToList[TSource](IEnumerable`1 source)
   at GitVersion.RepositoryStore.GetMergeCommitsForBranch(IBranch branch, Config configuration, IEnumerable`1 excludedBranches) in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Core\RepositoryStore.cs:line 438
   at GitVersion.RepositoryStore.FindCommitBranchWasBranchedFrom(IBranch branch, Config configuration, IBranch[] excludedBranches) in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Core\RepositoryStore.cs:line 320
   at GitVersion.Configuration.BranchConfigurationCalculator.InheritBranchConfiguration(IBranch targetBranch, BranchConfig branchConfiguration, ICommit currentCommit, Config configuration, IList`1 excludedInheritBranches)
   at GitVersion.Configuration.BranchConfigurationCalculator.GetBranchConfiguration(IBranch targetBranch, ICommit currentCommit, Config configuration, IList`1 excludedInheritBranches) in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Configuration\BranchConfigurationCalculator.cs:line 44
   at GitVersion.GitVersionContextFactory.Create(GitVersionOptions gitVersionOptions) in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Core\GitVersionContextFactory.cs:line 39
   at GitVersion.GitVersionCoreModule.<>c__DisplayClass0_0.<RegisterTypes>b__1() in D:\a\GitVersion\GitVersion\src\GitVersion.Core\GitVersionCoreModule.cs:line 37
   at System.Lazy`1.ViaFactory(LazyThreadSafetyMode mode)
   at System.Lazy`1.ExecutionAndPublication(LazyHelper executionAndPublication, Boolean useDefaultConstructor)
   at System.Lazy`1.CreateValue()
   at System.Lazy`1.get_Value()
   at GitVersion.VersionCalculation.NextVersionCalculator.get_context() in D:\a\GitVersion\GitVersion\src\GitVersion.Core\VersionCalculation\NextVersionCalculator.cs:line 15
   at GitVersion.VersionCalculation.NextVersionCalculator.FindVersion() in D:\a\GitVersion\GitVersion\src\GitVersion.Core\VersionCalculation\NextVersionCalculator.cs:line 30
   at GitVersion.GitVersionCalculateTool.CalculateVersionVariables() in D:\a\GitVersion\GitVersion\src\GitVersion.Core\Core\GitVersionCalculateTool.cs:line 51
   at GitVersion.GitVersionExecutor.RunGitVersionTool(GitVersionOptions gitVersionOptions) in D:\a\GitVersion\GitVersion\src\GitVersion.App\GitVersionExecutor.cs:line 66
  INFO [01/19/22 20:27:57:51] Attempting to show the current git graph (please include in issue):
  INFO [01/19/22 20:27:57:51] Showing max of 100 commits
  INFO [01/19/22 20:27:57:56] * 73f3620 11 seconds ago  (HEAD -> issue-branch, origin/issue-branch)
* 16f1f6d 8 minutes ago  (tag: state, origin/master, origin/HEAD, reproduce-issue, master)
* 007b77a 11 minutes ago
```