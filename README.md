# Battleship-field-validator
codewars 3 kyu
### DESCRIPTION:
Write a method that takes a field for well-known board game "Battleship" as an argument and returns true if it has a valid disposition of ships, false otherwise. Argument is guaranteed to be 10*10 two-dimension array. Elements in the array are numbers, 0 if the cell is free and 1 if occupied by ship.

**Battleship**  (also Battleships or Sea Battle) is a guessing game for two players. Each player has a 10x10 grid containing several "ships" and objective is to destroy enemy's forces by targetting individual cells on his field. The ship occupies one or more cells in the grid. Size and number of ships may differ from version to version. In this kata we will use Soviet/Russian version of the game.
![IWxeRBV](https://github.com/pcapo-dawi/Battleship-field-validator/assets/146750011/c56d0301-3dff-47c8-9a66-6a9a50bfd579)

Before the game begins, players set up the board and place the ships accordingly to the following rules:  

-   There must be single battleship (size of 4 cells), 2 cruisers (size 3), 3 destroyers (size 2) and 4 submarines (size 1). Any additional ships are not allowed, as well as missing ships.
-   Each ship must be a straight line, except for submarines, which are just single cell.
  
![FleBpT9](https://github.com/pcapo-dawi/Battleship-field-validator/assets/146750011/90469339-95b8-4390-87ed-6b01f015b46d)

- The ship cannot overlap or be in contact with any other ship, neither by edge nor by corner.
  
![MuLvnug](https://github.com/pcapo-dawi/Battleship-field-validator/assets/146750011/975f744c-b323-4cc4-b63b-91e4c6e02d1f)

## Code
````
public class BattleField {
    public static Integer comprobar(int x, int y, int[][] field) {

        if ((x > 0) && (y < 9))
            if (field[x - 1][y + 1] == 1) return 5;
        if ((x < 9) && (y < 9)) {
            if (field[x + 1][y + 1] == 1) return 5;
            if ((field[x + 1][y] == 1) && (field[x][y + 1] == 1)) return 5;
        }
        if (y < 9)
            if (field[x][y + 1] == 1) return 1 + comprobar(x, y + 1, field);

        if (x < 9)
            if (field[x + 1][y] == 1) return 1 + comprobar(x + 1, y, field);

        return 1;
    }
    public static boolean fieldValidator(int[][] field) {
        // your code here!
        Integer submarines = 0;
        int cruisers = 0;
        int destroyers = 0;
        int battleship = 0;
        for (int y = 0; y < 10; y++)
            for (int x = 0; x < 10; x++) {


                if (field[x][y] == 1) {
                    if ((x > 0) && (field[x - 1][y] == 1)) continue;
                    if ((y > 0) && (field[x][y - 1] == 1)) continue;


                    switch (comprobar(x, y, field)) {
                        case 1:
                            submarines++;
                            break;
                        case 2:
                            destroyers++;
                            break;
                        case 3:
                            cruisers++;
                            break;
                        case 4:
                            battleship++;
                            break;
                        default:
                            return false;
                    }
                }
            }
        System.out.println(destroyers);

        if (submarines != 4) return false;
        if (destroyers != 3) return false;
        if (cruisers != 2) return false;
        if (battleship != 1) return false;

        return true;
    }
}
