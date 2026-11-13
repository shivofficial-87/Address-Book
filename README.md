
#!/bin/bash

FILE="addressbook.txt"

while true
do
    echo " "
    echo "----- ADDRESS BOOK -----"
    echo "1. Create Address Book"
    echo "2. View Address Book"
    echo "3. Insert a Record"
    echo "4. Delete a Record"
    echo "5. Modify a Record"
    echo "6. Exit"

    read -p "Enter your choice: " ch

    case $ch in

    1)
        touch "$FILE"
        echo "Address Book Created Successfully"
        ;;

    2)
        if [ -s "$FILE" ]; then
            cat "$FILE"
        else
            echo "Address Book is Empty"
        fi
        ;;

    3)
        read -p "Enter Name: " name
        read -p "Enter Phone: " phone
        read -p "Enter Address: " address

        echo "$name | $phone | $address" >> "$FILE"
        echo "Record Inserted Successfully"
        ;;

    4)
        read -p "Enter Name to Delete: " name

        grep -v "^$name |" "$FILE" > temp.txt
        mv temp.txt "$FILE"

        echo "Record Deleted Successfully"
        ;;

    5)
        read -p "Enter Name to Modify: " name

        grep -v "^$name |" "$FILE" > temp.txt

        read -p "Enter New Name: " newname
        read -p "Enter New Phone: " newphone
        read -p "Enter New Address: " newaddress

        echo "$newname | $newphone | $newaddress" >> temp.txt

        mv temp.txt "$FILE"

        echo "Record Modified Successfully"
        ;;

    6)
        echo "Exiting Address Book"
        exit
        ;;

    *)
        echo "Invalid Choice"
        ;;

    esac
done
