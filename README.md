# NAME

fmg\_meta - register and assign meta fields and meta variables on a FortManager

# VERSION

version .1 (BETA)

# SYNOPSIS

```sh
# Register the definitions and assignments against an FMG 
./fmg_meta --fmg https://fmg.i.foletta.xyz meta.json

# Insecure if the certificate is not trusted
./fmg_meta --insecure --fmg https://fmg.i.foletta.xyz meta.json

# API user/pass can be specified as ENV vars
export FMG_API_USER=api_user
export FMG_API_PASS=c0mpl3xp4ssw0rd
./fmg_meta --fmg https://fmg.i.foletta.xyz meta.json

# Or on the command line (--username and --password work as well)
./fmg_meta --u api_user -p c0mpl3xp4ssw0rd --fmg https://fmg.i.foletta.xyz meta.json
 ```

# OPTIONS

- -f|--fmg _uri_ - the URI of the FortiManager API
- -u|--username _user_ - the FortiManager API username
- -p|--password _pass_ - the FortiManager API password
- -k|--insecure - don't verify certificate 
- -h|--help - print usage information

# BETA NOTES

Please note that this script is currently in beta. Two main things to take into account:

- The schema of the JSON file you use to define/apply the meta fields/variables may change at any time.
- It only supports defining and assigning meta fields, not meta variables (which are new in 7.2).

# REQUIREMENTS

You'll need the following modules, preferably installed using the more modern [cpanminus](https://metacpan.org/pod/App::cpanminus):

    sh$ cpanm Mojo::UserAgent

or the old CPAN client:

    sh$ cpan Mojo::UserAgent

# JSON DEFINITION

A an example `meta.json` file has been included in this repository.

# AUTHENTICATION

Once you have defined you API user on the FortiManager, the script will search for the credentials in three places:

- In $HOME/.ftnt/fmg\_api formatted as &lt;username>:&lt;password>
    - Lines beginning with '#' are skipped
- In the environment variabes `FMG_API_USER` and `FMG_API_PASS`
- In the command line arguments `-u|--username` and `-p|--password`.

If the credentials are available in multiple places, local dotfile beats environment variable beats commandline.
