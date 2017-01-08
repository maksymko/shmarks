# shmarks

Dead simple bash (sh?) bookmarks system, which completion.

## Installation

Copy _bash_shmarks file to your $HOME dir. I prefer prefixing the name with dot,
so that it would stay hidden.

```
cp _bash_shmarks $HOME/.bash_shmarks
```

Add this to your .bashrc:

```
export SHMARKS_DIR=$HOME/.bash_bookmarks
if test -f $HOME/.bash_shmarks; then
    . $HOME/.bash_shmarks
fi
```

You can change the value for SHMARKS_DIR, or even omit that line,
in which case `$HOME/.bookmarks` will be used.

## Usage

To bookmark your current directory:

```
mark bookmark_name
```

To see the list of bookmarks:

```
lsmarks
```

This will actually just an alias for `ls -l $SHMARKS_DIR`

To go to the bookmarked directory:

```
go bookmark_name
```

You can hit <Tab> for autocompletion.

I didn't add a special command to remove bookmarks. Mostly because I don't do it often :)
You can just delete symlink, if you no longer need it:

```
rm $SHMARKS_DIR/bookmark_name
```

## How it works

It created a directory $SHMARKS_DIR, where it then creates symlinks -- bookmarks.
The key to the whole thing is basically "-P" flag to `cd` command, which makes
it read symlink and go to that directory rather than making it look like you are
in SYMLINK_NAME directory.

That's it!
