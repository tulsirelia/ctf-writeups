## This is the question:
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?
Connect to fickle-tempest.picoctf.net 50705.

## My thought process
now since the problem provides a host a port, figured out i should use netcat.
so I did:

```bash
nc fickle-tempest.picoctf.net 50705
```
`Just letting you know Tulsi, netcat or nc, any of them can be used.`

The output was something like this:

<img width="638" height="677" alt="image" src="https://github.com/user-attachments/assets/40a0608a-13d5-422e-b3bb-b99aff144ac9" />

And ON and ON...

**HUH! As if they can trick me 😎**

I  understood the assignment, that the flag must be hidden in this long and cluttered text.
So i thought to save this text somewhere, to find the flag using grep

```bash
cp fickle-tempest.picoctf.net 50705 plumbing.txt
```
**Excellent Job!!** 
Error occurred, `cp: target 'plumbing.txt' is not a directory`
### cp command
```bash
cp [Source] [Source]...[Destination]
```
Last argument is the destination, but when the sources are > 1, the destination is expected to be a directory, and hence the description of the error.

Also, Tulsi the host and the port number are not any files for which you are using cp 😭

### Right Command

```bash
nc fickle-tempest.picoctf.net 50705 > plumbing.txt
```
Now, I have the text in plumbing.txt file

Next, I did:
```bash
strings plumbing.txt | grep "picoCTF"
```
Output of the grep "picoCTF" was positive, it said that the string matched from the file
But it has to be extracted by strings command...

"I could simply do grep "picoCTF" plumbing.txt", instead of overcomplicating it using strings command, it is not a binary file, C'mon!"
Since the challenge is called **plumbing**, I'd explicitly connect it to Linux pipes

**WooHoo!!**
```text
picoCTF{digital_plumb3r_00da27CC}
```
And the simplest solution to the whole problem was just one command:\
```bash
nc fickle-tempest.picoctf.net 50705 | grep "picoCTF"
```

EASY PEASY!! LEMON SQEEZY!!😁


