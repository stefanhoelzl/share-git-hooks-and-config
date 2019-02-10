# share your git hooks and config

How to share your git hooks and config with your team members 
and put them under version control

## Demo
```bash
# change your 'core.hookspath' to the tracked 'hooks' directory
$ git config --global core.hookspath hooks

# clone the repository
$ git clone https://github.com/stefanhoelzl/commit-git-hooks-and-config
$ cd commit-git-hooks-and-config

# use the custom alias defined in .gitconfig
$ git head-ref
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx refs/remotes/origin/HEAD

# use the custom pre-commit hook in hooks
$ touch test
$ git commit -a -m"test git hook"
About to commit using tracked git hook
[master d330c48] test git hook
 1 file changed, 1 insertion(+), 1 deletion(-)
```


## Details
### Let's start with the git hooks
Since it would be a security vulnerability
to just allow random git hooks to be executed on your system we need to set one
global git configuration value:

`git config --global core.hookspath <your-hooks-path>`

where `<your-hooks-path>` is relative to your repository root. This allows 
git hooks to be stored in a tracked directory. You can also save this in your 
local config, but then you have to set it for every repository you clone.

Now you can put all your git hooks into `<your-hooks-path>` and have them tracked
and shared with your team members.

> To be sure there is no malicous software hidden in the hooks coming with this
> repository check them out in `hooks` directory.

### How to use this to share our git configuration?
Now that we can have a shared `post-checkout` git hook we can use this to set a
`include.path` to our custom git configuration file.

So create a `post-checkout` hooks in `<your-hooks-path>`:
```
# content of <your-hooks-path>/post-checkout
git config --local include.path ../<your-gitconfig>
```

Now you can create a `<your-gitconfig>` file in your repo and the `post-checout`
hook will enforce that your team members work every time with the correct gitconfig.