# NAME

Mojolicious::Plugin::AutoSecrets - Automatic, Rotating Mojolicious Secrets

# SYNOPSIS

    # Mojolicious
    $self->plugin('AutoSecrets');

    $self->plugin('AutoSecrets' => {path => '/my/favorite/hiding/spot'});

    # Mojolicious::Lite
    plugin 'AutoSecrets';

# DESCRIPTION

[Mojolicious::Plugin::AutoSecrets](https://metacpan.org/pod/Mojolicious::Plugin::AutoSecrets) is a [Mojolicious](https://metacpan.org/pod/Mojolicious) plugin that takes care
of generating, storing, and rotating your ["secrets" in Mojolicious](https://metacpan.org/pod/Mojolicious#secrets).

## WARNING

Secrets are used to ensure integrity and trust [Mojolicious](https://metacpan.org/pod/Mojolicious) default session
cookies.  Letting code manage them means that code becomes part of your
security.  Read this documentation and review this code!

Take it from me, never trust a programmer.

# OVERVIEW

[Mojolicious::Plugin::AutoSecrets](https://metacpan.org/pod/Mojolicious::Plugin::AutoSecrets) requires no configuration, but does support
a few options:

## path

Default: `.mojo-secrets` in ["home" in Mojolicious](https://metacpan.org/pod/Mojolicious#home)

Accepts any file path for storing secrets and checking age.  It will be created
if it doesn't exist.

## mode

Default: `0600`

The file mode set when creating ["path"](#path).

## expire\_days

Default: `60`

After ["expire\_days"](#expire_days) days, generate a new secret and add it to the front of
the list.

## prune

Default: `3`

The secrets list will be pruned to this size as it is rotated.

## generator

Default: `Mojolicious::Plugin::AutoSecrets::generator`

Allows specifying a code ref that will be invoked with no arguments to generate
a new secret when necessary.

# INHERITANCE

[Mojolicious::Plugin::AutoSecrets](https://metacpan.org/pod/Mojolicious::Plugin::AutoSecrets) inherits all methods and attributes from
[Mojolicious::Plugin](https://metacpan.org/pod/Mojolicious::Plugin) and implements the following.

# METHODS

## register

    $plugin->register(Mojolicious->new);

Register plugin in [Mojolicious](https://metacpan.org/pod/Mojolicious) application.  Upon registration, this plugin
will generate, and store and rotate if necessary, secrets for the application.
An optional config hashref may tweak behavior, see ["OVERVIEW"](#overview).

If there are secrets already set at the time register executes, those secrets
**will not** be stored as managed secrets in ["path"](#path), and managed secrets will
be placed **before** existing secrets.  This should make it easy to move to or
from AutoSecrets.

# FUNCTIONS

## generator

The default secret generator, using Session::Token

# SEE ALSO

- [Mojolicious](https://metacpan.org/pod/Mojolicious)
- [Mojolicious::Sessions](https://metacpan.org/pod/Mojolicious::Sessions)
- ["signed\_cookie" in Mojolicious::Controller](https://metacpan.org/pod/Mojolicious::Controller#signed_cookie)

# AUTHOR

Meredith Howard <mhoward@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2018 by Meredith Howard.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
