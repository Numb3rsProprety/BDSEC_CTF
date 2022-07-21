

# Awesome Note Keeping 



- Category: `Web`
- Points: `100` => `100`
- Difficulty: Medium
- Solves: `235`


**Description**

> Un site ou l'on peut enregister et lire des notes.
> Auteur : NomanProdhan




### :book: Introduction





 
Le site est très simple, nous avons 2 fonctionnalités disponible: 
  - Enregister des notes en lui donnant un nom et du contenu
  - Lire une note à partir de son nom. 



Je commence par me dire que c'est une SQL Injectiokn donc j'injecte ' OR 1=1 -- - , " OR 1=1 -- - mais rien
n'y fait ça ne marche pas. Puis je pense à une SSTI (Server Side Template Injection) et j'injecte {{1+1}} mais
comme pour la SQLI ça ne marche pas. Je  commence à trifouiller les requêtes et je me rend compte que il y avait
tout simplement un fichier index.php.bak qui contient le code source de la page.

``` 
<!DOCTYPE html>
<html>

<head>
    <title>Awesome Note Keeping</title>
</head>

<body style="padding: 100px; background: #000000; color: #09b576">

    <h1>Welcome to Awesome Note Keeping</h1>
    <?php
    ini_set('display_errors', 1);
    ini_set('display_startup_errors', 1);
    error_reporting(E_ALL);
    if (isset($_POST["note"]) && isset($_POST["note_title"])) {
        if (empty($_POST["note"]) || empty($_POST["note_title"])) {
            echo "All fields are required.";
        } else if (strlen($_POST["note_title"]) >= 13) {
            echo "Note title is too long.";
        } else if (strlen($_POST["note"]) >= 40) {
            echo "Note is too long.";
        } else {
            $note_title = str_replace("flag", "", $_POST["note_title"]);
            if (!empty($note_title)) {
                if (file_exists($note_title . ".txt")) {
                    echo "There is already a note with that title and the note is <br>";
                    $note_title = str_replace("flag", "", $note_title);
                    $myNote = fopen($note_title . ".txt", "r");
                    echo fread($myNote, filesize($note_title . ".txt"));
                    fclose($myNote);
                } else {
                    $myNote = fopen($note_title . ".txt", "w");
                    fwrite($myNote, $_POST["note"]);
                    fclose($myNote);
                    echo "Your note has been saved.";
                }
            } else {
                echo "Sorry ! You can't create flag note.";
            }
        }
    }


    if (isset($_GET["note_title"]) && !empty($_GET["note_title"]) && $_GET["note_title"] != "flag") {
        if (file_exists($_GET["note_title"] . ".txt")) {
            $myNote = fopen($_GET["note_title"] . ".txt", "r");
            echo fread($myNote, filesize($_GET["note_title"] . ".txt"));
            fclose($myNote);
        } else {
            echo "Sorry ! Couldn't find any note with that title.";
        }
    }

    ?>
    <br>
    <h5>Create a Note</h5>
    <form action="" method="POST">
        <table>
            <tr>
                <td><label>Note Title : </label></td>
                <td><input type="text" name="note_title" /></td>
            </tr>
            <tr>
                <td><label>Note : </label></td>
                <td><textarea name="note"></textarea></td>
            </tr>
        </table>
        <input type="submit" value="Save" />
    </form>

    <h5>Read a Note</h5>
    <form action="" method="GET">
        <table>
            <tr>
                <td><label>Note Title : </label></td>
                <td><input type="text" name="note_title" /></td>
            </tr>
        </table>
        <input type="submit" value="Read" />
    </form>
    <!-- Hi Seli, I have created this awesome note keeping web app today. I have saved a backup file index.php.bak for you. Download it and check it out.  -->
</body>

</html>
```

N'étant pas très familier avec le PHP je lis le code pendant 10 minutes et je finit pas comprendre comment il marche.
Il vérifie d'abord que un paramètre note_title est donnée dans l'url. La longueur du titre et le contenu de la note sont
aussi limités. Le programme fait en sorte que lorsqu'une note est crée elle est enregistré dans un fichier txt avec son 
nom. Si on essaye d'enregister une note qui existe deja alors elle lit le contenu de la note mais si
le paramètre note_title est égal à flag alors il est remplacé par du vide. Puis il y a un deuxième str_replace
 qui remplace encore une fois "flag" par du vide. La dernière fonction permet de lire des notes a partir de leur nom mais
 elle nous interesse moins par ce que elle lit directement le paramètre note_title sans filtre et ne le modifie pas.
 



**Description**

Pour exploiter le code il suffit d'essayer d'enregistrer une note nommée "flflflagagag" car dans le premier str_replace
il y aura une seule occurence de flag puis dans le deuxieme str_replace étant donné que on a enlevé le "flag" à
note_title la variable est égal à flflagag et encore une fois flag est remplacé par du vide pour laisser finalement
flag et permettre au programme d'aller lire le fichier flag.txt et de nous donner le flag.



BDSEC{tHe_n0t3_K33p1n6_4W350M3_N5} 




