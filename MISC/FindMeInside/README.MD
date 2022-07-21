

# Find Me Inside 



- Category: `Misc`
- Points: `50` => `50`
- Difficulty: Easy
- Solves: `178`


**Description**

>I'm stuck in the dark
>
> Auteur : Typhlos#9037
>


**Attachments**

- `fireflies.gif`
- https://drive.google.com/drive/folders/1pz__cKtaR2zGI4AKjq8rmA2Sz0JSONHv?usp=sharing

### :book: Introduction


**Overview**

Le fichier en pièce jointe est simplement un gif du tombeau des lucioles. Je commence par inverser
inverser les couleurs du gif pour essyer de trouver un flag caché puis je me suis souvenu que ce 
n'était pas de la steg donc j'ai juste essayé un  ```7z e fireflies.gif``` et je me retrouve avec un fichier
nommée cry100 qui contient des chaines de char dont notamment une qui à attiré mon attention:
YWHVX{N33n_gsv_yfggviuob_tlvh_fk_fk_zmw_zdzb}
je cours sur https://www.dcode.fr/identification-chiffrement et pof c'est enfait un "chiffrement"
(a prendre avec des pincettes) nommé At Bash. Je decode le tout toujours avec dcode et hop on a le flag.

BDSEC{M33m_the_butterfly_goes_up_up_and_away}


