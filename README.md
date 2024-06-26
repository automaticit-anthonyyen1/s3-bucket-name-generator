# s3-bucket-name-generator
Generate an S3 bucket name that is hard to guess to mitigate DoS billing attack discussed in below article and thread.  
  
# Usage
```
s3-bucket-name-generator.sh [ -t ]  
```
# OPTION  
<dl>
  <dt>-t</dt>
  <dd>Enforce S3 bucket name restriction when using Amazon S3 Transfer Acceleration, that is, no dots (.) allowed.</dd>
</dl>

References:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[How an empty S3 bucket can make your AWS bill explode | by Maciej Pocwierz | Apr, 2024 | Medium](https://medium.com/@maciej.pocwierz/how-an-empty-s3-bucket-can-make-your-aws-bill-explode-934a383cb8b1)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[How an empty S3 bucket can make your AWS bill explode | Hacker News](https://news.ycombinator.com/item?id=40203126)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Bucket naming rules - Amazon Simple Storage Service](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucketnamingrules.html)  

Using [Password Strength Tester](https://alecmccutcheon.github.io/Password-Entropy-Calculator/) with a randomly-selected password
generated by this tool, we can roughly expect about 290 entropy bits as calculated by Claude Shannon's way of calculating it, 370
entropy bits as calculated by the trigraph way of calculating it. 60-70 entropy bits is generally considered very strong, so this
should be sufficient until cloud providers deliver a stronger defense.

Requires makepasswd(1) tool at [khorben/makepasswd: Makepasswd generates (pseudo-)random passwords of a desired length](https://github.com/khorben/makepasswd/), which is available in many Linux distributions.

In Red Hat Enterprise Linux, CentOS, Rocky Linux, Fedora and distributions that use ``dnf``:  
```shell
sudo dnf install makepasswd
```
In Debian, Ubuntu, Mint, Elementary OS and distributions that use ``apt-get``:  
```shell
sudo apt-get install makepasswd
```
In Arch Linux, Manjaro and distributions that use ``pacman``:  
```shell
sudo pacman -S makepasswd
```

As of April 2024, we could not find makepasswd in NixOS packages searching at:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;https://search.nixos.org/packages?channel=23.11&from=0&size=50&sort=relevance&type=packages&query=makepasswd  
Under NixOS, makepasswd(1) might need to be built and packaged from source. We opened Issue  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;https://github.com/NixOS/nixpkgs/issues/308030  
requesting packaging of makepasswd(1). Also not found in Homebrew at https://formulae.brew.sh/.

# INSTALL
Copy down [``s3-bucket-name-generator.sh``](https://raw.githubusercontent.com/automaticit-anthonyyen1/s3-bucket-name-generator/main/s3-bucket-name-generator.sh)
to your computer, set execute permission bits with ``chmod u+x s3-bucket-name-generator.sh``, and execute with ``./s3-bucket-name-generator.sh``. We expect this
attack vector will be mitigated relatively promptly, so didn't bother packaging for easier installation, but welcome Pull Requests that implement the packaging
if others submit them.
