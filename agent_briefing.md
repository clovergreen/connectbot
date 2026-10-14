1. project summary:
2. project directory:
3. conda environment under project directory:
4. reference documents under project directory:
5. write progress of each task in notes/agent_progress.md with title and time. Create it if not existing.
6. commit to git for task that modify/add/delete source files
7. create new branch from current if it is another bug or another feature
8. how to full build?
9. how to partial build?
10. build and test lock rule:
    Before build/test work, acquire the persistent lock with a unique caller or
    session name. Repeated calls by the same owner are allowed; other names are
    rejected with status 75 until the owner releases the lock.
        ./run_locked.sh <session-name>
    Run commands as that owner:
        ./run_locked.sh <session-name> <command> [args...]
    Examples:
        ./run_locked.sh agent-1 make -j4
        ./run_locked.sh agent-1 pytest tests/
    After all related work is finished, the owner must release it explicitly:
        ./run_locked.sh agent-1 release
    If the owner cannot release it because of a crash or machine error, recover
    with the following command. Never use it while the owner is still active:
        ./run_locked.sh force_release
