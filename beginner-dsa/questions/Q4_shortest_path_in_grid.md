import java.util.*;

public class ShortestPathInGrid {
    static class Cell {
        int row, col, dist;
        Cell(int row, int col, int dist) {
            this.row = row;
            this.col = col;
            this.dist = dist;
        }
    }

    public int shortestPath(int[][] grid, int[] start, int[] end) {
        int m = grid.length;
        int n = grid[0].length;
        boolean[][] visited = new boolean[m][n];
        int[] dr = { -1, 1, 0, 0 };
        int[] dc = { 0, 0, -1, 1 };

        Queue<Cell> q = new LinkedList<>();
        q.offer(new Cell(start[0], start[1], 0));
        visited[start[0]][start[1]] = true;

        while (!q.isEmpty()) {
            Cell curr = q.poll();
            if (curr.row == end[0] && curr.col == end[1]) {
                return curr.dist;
            }
            for (int d = 0; d < 4; d++) {
                int nr = curr.row + dr[d];
                int nc = curr.col + dc[d];
                if (nr >= 0 && nr < m && nc >= 0 && nc < n &&
                    !visited[nr][nc] && grid[nr][nc] == 0) // assuming 0 is open, 1 is wall
                {
                    visited[nr][nc] = true;
                    q.offer(new Cell(nr, nc, curr.dist + 1));
                }
            }
        }
        return -1;
    }
}
