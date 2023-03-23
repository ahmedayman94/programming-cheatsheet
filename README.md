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
## Git squash commits
```
git rebase -i HEAD~2
// Where 2 is number of commits to squash.
// In interactive mode, choose the commits to squash with 'fixup'
```
# Linux/Shell commands
## Find all devices on a network
```
arp -a
```
## Shell find and replace (sed)
- To find and replace "_" with "-"
```
echo "Hello_World" | sed 's/_/-/g'
```
where s indicates find and replace
- To find and replace in file
```
sed -i 's/word1/word2/g' file.txt
```
where i indicates to edit the file and save it
## grep to find word in file
```
// grep <keyword> <filename>
grep version package.json
```

## SSH Port forwarding
If we have a VM that acts as an SSH server and we want to access a private database (cosmos for e.g)

```
ssh -L 127.0.0.1:443:cosmos-dns-name.com:443 usernameToVM@<VM-IP-v4-Address> -vvv
```
This runs a local server that will forward HTTP traffic via SSH to the VM
* `-vvv` is verbose mode
** We might need to edit hosts file to resolve the dns name to loopback address
## base64
```
echo -n "somethings that i want to convert to basesixtyfour" | base64
```
where `-n` flag in the echo terminates with an empty line `\n`

## Find my public ip address
```
curl ifconfig.co
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
## nginx conf: Reverse proxy multiple domains
```
// This will route any request to the localhost domain to targetdomain1
server {
    listen       80;
    listen  [::]:80;
    server_name localhost;

    location / {
        proxy_pass https://targetdomain1/;
    }
}

// This will route any request to myapp.com to targetdomain2
// For e.g request to myapp.com/users/userId will be proxied to https://targetdomain2/users/userId
// The client will only establish a connection to the nginx reverse proxy, unaware of targetdomain2
server {
    listen       80;
    listen  [::]:80;
    server_name myapp.com;

    location / {
        proxy_pass https://targetdomain2/;
    }
    
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
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
## CORS
Cors only becomes an issue in the browser when the request has the "origin" header, because then the "Access-Control-Allow-Origin" header is read by the browser before deciding on allowing or denying the response.
Typically, css or html files in the DOM do not send this origin header, therefore they wont face issues with CORS.
However, using "fetch" to get those files would include the Origin header in the request, as well as loading fonts (via css for example).
