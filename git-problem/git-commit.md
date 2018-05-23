###
To https://github.com/zzqfighting/develop-problem.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/zzqfighting/develop-problem.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

1.  诱发原因：本地新建仓库第一次向远程提交
1.  解决方案：git push origin master -f，强行让本地分支覆盖远程分支