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

    // Directions: up, down, left, right
    private static final int[][] directions = {
        {-1, 0}, {1, 0}, {0, -1}, {0, 1}
    };

    public static int shortestPath(int[][] grid, int[] start, int[] end) {
        int m = grid.length, n = grid[0].length;
        boolean[][] visited = new boolean[m][n];
        Queue<Cell> queue = new LinkedList<>();

        queue.offer(new Cell(start[0], start[1], 0));
        visited[start[0]][start[1]] = true;

        while (!queue.isEmpty()) {
            Cell current = queue.poll();

            // If we reach the destination
            if (current.row == end[0] && current.col == end[1])
