# Git commands
## Git stash only unstaged changes
```
git add <files><to> <stage>
git stash push --keep-index
```
## Git revert commit before push
```
git reset HEAD~1
```
## Git reset branch to master
```
git reset --hard origin/master
git push -f
```
# Linux/Shell commands
## Find all devices on a network
```
arp -a
```
## Shell find and replace (sed)
- To find and replace "_" with "-"
```
echo "Hello_World" | sed 's/_/-g'
```
where s indicates find and replace
- To find and replace in file
```
sed 's/word1/word2/g' file.txt
```

# Other
## Regex match up to and excluding a character
- Input: /categories/3/posts/2
- Desired match: "3"
```
(?<=categories\\/)((.*?(?=\\/))
/**
 * Explanation: ?<= is positive lookbehind, .*? is match and stop after one discovery. Lastly, ?= is a positive look ahead.
 * By combining both lookbehind and ( lookahead, we can capture the sandwiched result which is 3 in this case, that is between the categories/ and the /posts.
**/
```
## Node command to get package name and version
```
node -pe "require('./package.json').version
node -pe "require('./package.json').name
```
where -p prints and -e evalutes

## Docker run container from image without stopping
If you try to run a container from an image, and that image does not persist (i.e a script that finishes), then the container will exit. It becomes impossible to bash into the container and check things out (version of node for e.g).
To remedy that, and keep the container running, do the following:
```
docker run -t -d <image-id>
```
Alternatively and a shortcut, do the following:
```
docker run -it <image-id> bash
```
## CSS: Target all child elements except the first
It can be useful in scenarios to set for example a border-top on all the child elements but it doesnt make sense to do that on the first one.
To solve this:
```
<style>
    .container > *:not(:first-child) {
tborder-top: 1px solid black;
    }
</style>
<div class="container">
  <div> Child one </div>
  <div> Child two </div>
  <div> Child three </div>
</div>
```
