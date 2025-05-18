<h1>Experiment No. 7: Implementation of Alpha-Beta Pruning in Minimax Search Algorithm for a Simple TIC-TAC-TOE Game</h1>

<h3>Name: Yuvarani T</h3>
<h3>Register Number: 212222110057</h3>

<h2>Aim:</h2>
<p>
To implement the Alpha-Beta Pruning technique in the Minimax Search Algorithm for a simple TIC-TAC-TOE game using Python.
</p>

<h2>Goals of Alpha-Beta Pruning in Minimax Search Algorithm:</h2>
<ul>
    <li>Enhance the decision-making efficiency of the computer player.</li>
    <li>Reduce the number of nodes evaluated in the game tree.</li>
</ul>

<p>
This project uses the Minimax algorithm combined with Alpha-Beta Pruning to allow the computer to evaluate the best move by analyzing possible game states. Alpha-Beta Pruning avoids exploring unnecessary branches, thereby improving performance.
</p>

<h2>The Minimax Algorithm:</h2>
<p>
The Minimax algorithm recursively evaluates all possible moves and their outcomes by creating a game tree. It assumes that the opponent will also play optimally.
</p>

<h2>Alpha-Beta Pruning:</h2>
<p>
The Alpha-Beta pruning algorithm improves the Minimax algorithm by eliminating branches in the game tree that do not influence the final decision. This pruning helps to reduce the computation time while ensuring the same result as the standard Minimax.
</p>
<hr>

<h2>Python Program:</h2>
<pre>
import time
class Game:
    def __init__(self):
        self.initialize_game()
    def initialize_game(self):
        self.current_state = [['.','.','.'],
                              ['.','.','.'],
                              ['.','.','.']]
        self.player_turn = 'X'
    def draw_board(self):
        for i in range(0, 3):
            for j in range(0, 3):
                print('{}|'.format(self.current_state[i][j]), end=" ")
            print()
        print()
    def is_valid(self, px, py):
        return 0 <= px <= 2 and 0 <= py <= 2 and self.current_state[px][py] == '.'
    def is_end(self):
        for i in range(3):
            if self.current_state[0][i] != '.' and \
               self.current_state[0][i] == self.current_state[1][i] == self.current_state[2][i]:
                return self.current_state[0][i]
            if self.current_state[i] == ['X', 'X', 'X']:
                return 'X'
            if self.current_state[i] == ['O', 'O', 'O']:
                return 'O'
        if self.current_state[0][0] != '.' and \
           self.current_state[0][0] == self.current_state[1][1] == self.current_state[2][2]:
            return self.current_state[0][0]
        if self.current_state[0][2] != '.' and \
           self.current_state[0][2] == self.current_state[1][1] == self.current_state[2][0]:
            return self.current_state[0][2]
        for row in self.current_state:
            if '.' in row:
                return None
        return '.'
    def max_alpha_beta(self, alpha, beta):
        maxv = -2
        px = py = None
        result = self.is_end()
        if result == 'X':
            return -1, 0, 0
        elif result == 'O':
            return 1, 0, 0
        elif result == '.':
            return 0, 0, 0
        for i in range(3):
            for j in range(3):
                if self.current_state[i][j] == '.':
                    self.current_state[i][j] = 'O'
                    m, _, _ = self.min_alpha_beta(alpha, beta)
                    self.current_state[i][j] = '.'
                    if m > maxv:
                        maxv = m
                        px, py = i, j
                    if maxv >= beta:
                        return maxv, px, py
                    if maxv > alpha:
                        alpha = maxv
        return maxv, px, py
    def min_alpha_beta(self, alpha, beta):
        minv = 2
        qx = qy = None
        result = self.is_end()
        if result == 'X':
            return -1, 0, 0
        elif result == 'O':
            return 1, 0, 0
        elif result == '.':
            return 0, 0, 0
        for i in range(3):
            for j in range(3):
                if self.current_state[i][j] == '.':
                    self.current_state[i][j] = 'X'
                    m, _, _ = self.max_alpha_beta(alpha, beta)
                    self.current_state[i][j] = '.'
                    if m < minv:
                        minv = m
                        qx, qy = i, j
                    if minv <= alpha:
                        return minv, qx, qy
                    if minv < beta:
                        beta = minv
        return minv, qx, qy
    def play_alpha_beta(self):
        while True:
            self.draw_board()
            result = self.is_end()
            if result:
                if result == 'X':
                    print('The winner is X!')
                elif result == 'O':
                    print('The winner is O!')
                else:
                    print("It's a tie!")
                break
            if self.player_turn == 'X':
                while True:
                    start = time.time()
                    _, qx, qy = self.min_alpha_beta(-2, 2)
                    end = time.time()
                    print(f'Evaluation time: {round(end - start, 7)}s')
                    print(f'Recommended move: X = {qx}, Y = {qy}')
                    px = int(input('Insert the X coordinate: '))
                    py = int(input('Insert the Y coordinate: '))
                    if self.is_valid(px, py):
                        self.current_state[px][py] = 'X'
                        self.player_turn = 'O'
                        break
                    else:
                        print('Invalid move! Try again.')
            else:
                _, px, py = self.max_alpha_beta(-2, 2)
                self.current_state[px][py] = 'O'
                self.player_turn = 'X'
def main():
    g = Game()
    g.play_alpha_beta()

if __name__ == "__main__":
    main()
</pre>

<h2>Sample Output Screenshots:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)

<h2>Output:</h2>

![{1DE42D09-C14A-4459-A4F6-8D5373840490}](https://github.com/user-attachments/assets/9a0d6b4c-7120-4b20-84d9-cafc485dccf4)
![{DAEFFDF3-DE56-43AA-842A-7619B8C1C614}](https://github.com/user-attachments/assets/133722a1-ddef-4a8c-afa3-f56bf3135670)

<h2>Result:</h2>
<p>
Thus, the implementation of Alpha-Beta Pruning in the Minimax Search Algorithm for a simple Tic-Tac-Toe game was successfully completed.
</p>
