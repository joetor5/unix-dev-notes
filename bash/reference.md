# Bash Reference

## Prompting the user

```sh
    while true; do
        read -p "The above good signatures were found. Do you trust some of these? [y/n]: " answer
        case $answer in
            Y|y)
                touch .sign_verified; break;;
            N|n)
                echo "Installation aborted: keys not trusted"; exit 1;;
        esac
    done
```
