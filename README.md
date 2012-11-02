# NAME

PPI::Transform::Sequence - Tiny binder to combine multiple PPI::Transform objects

# VERSION

version v0.0.0

# SYNOPSIS

    use PPI::Transform::Sequence;
    my $trans = PPI::Transform::Sequence->new(
      PPI::Transform::UpdateCopyright => [ name => 'Yasutaka ATARASHI' ],
      PPI::Transform::PackageName => [ -all => sub { s/^Acme\b/ACME/g } ],
    );

    print $trans->idx(0)->name; # access to PPI::Transform subclass object

    # All PPI::Transform methods can be called, and
    # Each transformation is sequentially applied.
    $trans->file('Change.pm'); # Update copyright, then package names are replaced

# DESCRIPTION

This module is a tiny binder to combine multiple [PPI::Transform](http://search.cpan.org/perldoc?PPI::Transform) objects into one [PPI::Transform](http://search.cpan.org/perldoc?PPI::Transform) object.
You can combine them in-place without writing specific modules.
Combined objects are sequentially applied.

# METHODS

All of [PPI::Transform](http://search.cpan.org/perldoc?PPI::Transform) methods are inherited.

## new(_list_)

_list_ is sequential pairs of a PPI::Transform subclass name and an array reference of constructor arguments.
Even though there is no argument or only one argument, it is necessary to specify an array reference.
The order of _list_ is used as the application order of [PPI::Transform](http://search.cpan.org/perldoc?PPI::Transform) objects.

## idx(_index_)

Accessor of combined objects. _index_ is a 0-based number in _list_, which are arguments of `new`.

# AUTHOR

Yasutaka ATARASHI <yakex@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2012 by Yasutaka ATARASHI.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
