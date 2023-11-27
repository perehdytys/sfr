#!/bin/sh
# sfr - remove files of certain extensions

[ -z "$1" ] && { printf '\n%s\n' "usage: sfr [EXTENSIONS]" ; exit ; }

tempfile=$(mktemp -t sfr.XXXXX)

while [ "$1" ]; do
    find . -name "*.$1" >> "$tempfile" 
    shift
done

[ -s "$tempfile" ] || { printf '\n%s\n' "no file was found" ; exit ; }

read -p "Remove the files without checking them[y/n]: " check

if [ "$check" != 'y' ]; then
    cat -n "$tempfile"
    echo
    read -p "Delete the files[y/n]: " check
fi

case $check in
    y)
        while IFS= read -r f; do
            rm "$f"
        done < "$tempfile"
        ;;
    *)
        printf '\n%s\n' "No file was removed"
        ;;
esac

exit
