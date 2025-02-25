gpublic class GameOfLife {

    public static void gameOfLife(int[][] board) {
        if (board == null || board.length == 0) return;

        int m = board.length;
        int n = board[0].length;

        // Создаем временную копию доски
        int[][] nextState = new int[m][n];

        // Определяем восемь возможных направлений для соседей
        int[] directions = {-1, 0, 1};

        // Проходим по каждой клетке доски
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                // Считаем количество живых соседей
                int liveNeighbors = 0;

                for (int x : directions) {
                    for (int y : directions) {
                        if (x == 0 && y == 0) continue; // Пропускаем текущую клетку

                        int newX = i + x;
                        int newY = j + y;

                        // Проверяем, что сосед находится в пределах доски
                        if (newX >= 0 && newX < m && newY >= 0 && newY < n && board[newX][newY] == 1) {
                            liveNeighbors++;
                        }
                    }
                }

                // Применяем правила игры
                if (board[i][j] == 1) {
                    if (liveNeighbors < 2 || liveNeighbors > 3) {
                        nextState[i][j] = 0; // Клетка умирает
                    } else {
                        nextState[i][j] = 1; // Клетка остается живой
                    }
                } else {
                    if (liveNeighbors == 3) {
                        nextState[i][j] = 1; // Клетка оживает
                    } else {
                        nextState[i][j] = 0; // Клетка остается мертвой
                    }
                }
            }
        }

        // Копируем следующее состояние в исходную доску
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                board[i][j] = nextState[i][j];
            }
        }
    }

    public static void printBoard(int[][] board) {
        for (int[] row : board) {
            for (int cell : row) {
                System.out.print(cell == 1 ? "■ " : "□ ");
            }
            System.out.println();
        }
        System.out.println();
    }

    public static void main(String[] args) throws InterruptedException {
        int[][] board = {
            {0, 1, 0},
            {0, 0, 1},
            {1, 1, 1},
            {0, 0, 0}
        };

        while (true) {
            printBoard(board);
            gameOfLife(board);
            Thread.sleep(1000); // Задержка в 1 секунду
        }
    }
}
