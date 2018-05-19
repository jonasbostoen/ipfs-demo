# IPFS Demo

Connect to the IPFS network with this Demo

### Dependencies

- [snapcraft](https://snapcraft.io/)
 \- For downloading the IPFS snap
- [IPFS](https://ipfs.io/)

```
$ sudo apt install snapd
$ snap install ipfs
```

You can also install ipfs with `$ go get ` for the Go daemon

### Process

Start by initializing your node, this will create a key-pair and a repository with a database of objects:
```
$ ipfs init
```

You now have your peer identity on the IPFS network. Use:

```
$ ipfs cat /ipfs/<your identity>/readme
```
You should see this:
```
Hello and Welcome to IPFS!

██╗██████╗ ███████╗███████╗
██║██╔══██╗██╔════╝██╔════╝
██║██████╔╝█████╗  ███████╗
██║██╔═══╝ ██╔══╝  ╚════██║
██║██║     ██║     ███████║
╚═╝╚═╝     ╚═╝     ╚══════╝

If you're seeing this, you have successfully installed
IPFS and are now interfacing with the ipfs merkledag!

 -------------------------------------------------------
| Warning:                                              |
|   This is alpha software. Use at your own discretion! |
|   Much is missing or lacking polish. There are bugs.  |
|   Not yet secure. Read the security notes for more.   |
 -------------------------------------------------------

Check out some of the other files in this directory:

  ./about
  ./help
  ./quick-start     <-- usage examples
  ./readme          <-- this file
  ./security-notes
```
You can go through the other files in the directory and explore the IPFS merkledag.

Let's now add a text file to the IPFS network:
```
$ echo "Your first file on IPFS!" > IPFSfile
$ ipfs add IPFSfile
```
This will generate a hash that will serve as the unique identifier for that file. Here we can see a clear difference with the standard http protocol: the files on IPFS are content based instead of location based. This means that you won't request something from an IP location - you will request the hash of a certain file.

Let's now take a look at our file, copy the hash that was returned to you and execute:
```
ipfs cat <hash>
```
This will return whatever text you put into that file!

If you wanted to add a whole directory, use:
```
$ ipfs add -r <path/to/directory>
```
This will generate unique hashes for every file in the repository, unless some files are the same.

Let's actually connect to the IPFS web:
```
$ ipfs daemon
```
See the details of your connection with `$ ipfs id`

To see who on the IPFS network you're connected to, check your peers:
```
$ ipfs swarm peers
```
Inspect any of your peers with `$ ipfs id <hash of peer>`

Now that we've initialized the daemon and are connected to the IPFS network, let's inspect our file through the http gateway. The default is localhost:8080.

Go to the browser and type in:
```
localhost:8080/ipfs/<hash of file>
```
You should now see simple HTML of whatever you've typed into the file. This works with all types of files, you can try it with an image or a video for example.

This might not seem that special though, since it's just on a localhost. IPFS has gateways however. Access it by searching in your browser:
```
gateway.ipfs.io/ipfs/<hash of file>
```
This will give the same output as the search above. The gateway sent a request to your node, pulled the file, and displayed it in your browser. And it was all pretty fast.

Now let's navigate to
```
127.0.0.1:5001/webui
```
This downloaded the entire web application from the network. This serves as an example of how you would deplay entirely distributed web applications. People who want to use it can then be provided with a link, which downloads the app and runs it locally for them.

Navigate through the web-app to see some cool stuff like your connections all around the world. It also serves as a graphical user interface of some sorts - if you navigate to "files" you can drag and drop files to automatically add them to the IPFS network.

Additional Material:
- Theoretical introduction: https://www.youtube.com/watch?v=5Uj6uR3fp-U
- Extensive theoretical exploration by founder Juan Benet: https://www.youtube.com/watch?v=HUVmypx9HGI

Also check out the whitepaper that I've put on IPFS:
- https://gateway.ipfs.io/ipfs/QmV9tSDx9UiPeWExXEeH6aoDvmihvx6jD5eLb4jbTaKGps
