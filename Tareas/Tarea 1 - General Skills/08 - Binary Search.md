# Binary Search

## Descripcion
Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools!You can download the challenge files here:

- [challenge.zip](https://artifacts.picoctf.net/c_atlas/20/challenge.zip)

`ssh -p 50317 ctf-player@atlas.picoctf.net`Using the password `6abf4a82`. Accept the fingerprint with `yes`, and `ls` once connected to begin. Remember, in a shell, passwords are hidden!
## Solucion
Descargamos el archivo para ver el codigo del reto que se esta corriendo en el servidor:
```

┌──(xrengariox㉿PC)-[~/Downloads/home/ctf-player/drop-in]
└─$ cato guessing_game.sh 

            #!/bin/bash

            # Generate a random number between 1 and 1000
            target=$(( (RANDOM % 1000) + 1 ))

            echo "Welcome to the Binary Search Game!"
            echo "I'm thinking of a number between 1 and 1000."

            # Trap signals to prevent exiting
            trap 'echo "Exiting is not allowed."' INT
            trap '' SIGQUIT
            trap '' SIGTSTP

            # Limit the player to 10 guesses
            MAX_GUESSES=10
            guess_count=0

            while (( guess_count < MAX_GUESSES )); do
                read -p "Enter your guess: " guess

                if ! [[ "$guess" =~ ^[0-9]+$ ]]; then
                    echo "Please enter a valid number."
                    continue
                fi

                (( guess_count++ ))

                if (( guess < target )); then
                    echo "Higher! Try again."
                elif (( guess > target )); then
                    echo "Lower! Try again."
                else
                    echo "Congratulations! You guessed the correct number: $target"

                    # Retrieve the flag from the metadata file
                    flag=$(cat /challenge/metadata.json | jq -r '.flag')
                    echo "Here's your flag: $flag"
                    exit 0  # Exit with success code
                fi
            done

            # Player has exceeded maximum guesses
            echo "Sorry, you've exceeded the maximum number of guesses."
            exit 1  # Exit with error code to close the connection

```

Y vemos quee basicamente tenemos que hacer una busqueda binaria, asi que nos conectamos al reto con las credenciales que nos dan:
```bash
ssh -p 50317 ctf-player@atlas.picoctf.net
```

Y comenzamos a buscar el numero
```bash
┌──(xrengariox㉿PC)-[~/Downloads/home/ctf-player/drop-in]
└─$ ssh -p 50317 ctf-player@atlas.picoctf.net
The authenticity of host '[atlas.picoctf.net]:50317 ([18.217.83.136]:50317)' can't be established.
ED25519 key fingerprint is SHA256:M8hXanE8l/Yzfs8iuxNsuFL4vCzCKEIlM/3hpO13tfQ.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[atlas.picoctf.net]:50317' (ED25519) to the list of known hosts.
ctf-player@atlas.picoctf.net's password: 
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Lower! Try again.
Enter your guess: 250
Lower! Try again.
Enter your guess: 125
Higher! Try again.
Enter your guess: 188
Higher! Try again.
Enter your guess: 220
Lower! Try again.
Enter your guess: 204
Higher! Try again.
Enter your guess: 212
Lower! Try again.
Enter your guess: 208
Higher! Try again.
Enter your guess: 210
Lower! Try again.
Enter your guess: 209
Congratulations! You guessed the correct number: 209
Here's your flag: picoCTF{g00d_gu355_bee04a2a}
Connection to atlas.picoctf.net closed.
```

Al acertar nos da la flag:
```
picoCTF{g00d_gu355_bee04a2a}
```

## Notas adicionales

## Referencias
