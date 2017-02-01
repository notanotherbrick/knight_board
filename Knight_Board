from collections import deque
import heapq


class Solution(object):
    def __init__(self,width):
        self.w = width

        if self.w == 32:
            board32_string = [
            '. . . . . . . . B . . . L L L . . . . . . . . . . . . . . . . .',
            '. . . . . . . . B . . . L L L . . . . . . . . . . . . . . . . .',
            '. . . . . . . . B . . . L L L . . . L L L . . . . . . . . . . .',
            '. . . . . . . . B . . . L L L . . L L L . . . R R . . . . . . .',
            '. . . . . . . . B . . . L L L L L L L L . . . R R . . . . . . .',
            '. . . . . . . . B . . . L L L L L L . . . . . . . . . . . . . .',
            '. . . . . . . . B . . . . . . . . . . . . R R . . . . . . . . .',
            '. . . . . . . . B B . . . . . . . . . . . R R . . . . . . . . .',
            '. . . . . . . . W B B . . . . . . . . . . . . . . . . . . . . .',
            '. . . R R . . . W W B B B B B B B B B B . . . . . . . . . . . .',
            '. . . R R . . . W W . . . . . . . . . B . . . . . . . . . . . .',
            '. . . . . . . . W W . . . . . . . . . B . . . . . . T . . . . .',
            '. . . W W W W W W W . . . . . . . . . B . . . . . . . . . . . .',
            '. . . W W W W W W W . . . . . . . . . B . . R R . . . . . . . .',
            '. . . W W . . . . . . . . . . B B B B B . . R R . W W W W W W W',
            '. . . W W . . . . . . . . . . B . . . . . . . . . W . . . . . .',
            'W W W W . . . . . . . . . . . B . . . W W W W W W W . . . . . .',
            '. . . W W W W W W W . . . . . B . . . . . . . . . . . . B B B B',
            '. . . W W W W W W W . . . . . B B B . . . . . . . . . . B . . .',
            '. . . W W W W W W W . . . . . . . B W W W W W W B B B B B . . .',
            '. . . W W W W W W W . . . . . . . B W W W W W W B . . . . . . .',
            '. . . . . . . . . . . B B B . . . . . . . . . . B B . . . . . .',
            '. . . . . R R . . . . B . . . . . . . . . . . . . B . . . . . .',
            '. . . . . R R . . . . B . . . . . . . . . . . . . B . T . . . .',
            '. . . . . . . . . . . B . . . . . R R . . . . . . B . . . . . .',
            '. . . . . . . . . . . B . . . . . R R . . . . . . . . . . . . .',
            '. . . . . . . . . . . B . . . . . . . . . . R R . . . . . . . .',
            '. . . . . . . . . . . B . . . . . . . . . . R R . . . . . . . .',
            '. . . . . . . . . . . B . . . . . . . . . . R R . . . . . . . .',
            '. . . . . . . . . . . B . . . . . . . . . . R R . . . . . . . .',
            '. . . . . . . . . . . B . . . . . . . . . . R R . . . . . . . .',
            '. . . . . . . . . . . B . . . . . . . . . . R R . . . . . . . .']
            #Convert board to 32x32 array
            self.board = [y.split(' ') for y in board32_string]


    def print_curr_board(self,curr):
        '''
        Prints the board with position corresponding to curr as 'K'
        Input
        curr : location of current square as [row,column]
        Output 
        return : NONE
        '''
        print '\n'
        print '    0  1  2  3  4  5  6  7'
        for i in xrange(self.w):
            print i, ' ',
            for j in xrange(self.w):
                if curr == [i, j]: 
                    print 'K ',
                else:
                    print '* ',
            print '\n' 


#seq32=[[-1]*8 for _ in xrange(8)]

    def is_valid_move(self,next_move, curr):
        '''
        Checks if next_move is valid for a Knight on the 32x32 chessboard
        For a move to be valid, Knight must move exactly 2 steps in one direction
        And exactly 1 step in the other direction

        Returns a boolean value based on above criteria

        Input 
        next_move : Next move on board in [row,col]
        curr      : Current position of Knight in [row,col]
        '''
        if self.is_valid_position(next_move): 
            dx = abs(next_move[0] - curr[0])
            dy = abs(next_move[1] - curr[1])
            # x+y =3, x*y = 2 has only (1,2) and (2,1)  as solutions
            return dx + dy == 3 and dx * dy == 2

    def is_valid_position(self,move):
        '''
        Checks if the move is valid for 32x32 board
        Checks include
        - move is a list of integers 
        - length of move is 2
        - row value lies in [0,7]
        - column value lies in [0,7]
        Returns a boolean value based on above criteria

        Input
        move : Move in [row,col]
        '''

        if (len(move)!=2 or
            type(move)!=list or
            type(move[0])!=int or
            type(move[1])!=int or
            move[0] >self.w-1 or
            move[0]<0 or
            move[1] >self.w-1 or
            move[1]<0):
            return False

        if self.w == 32:
            if (self.board[move[0]][move[1]] == 'B' or
                self.board[move[0]][move[1]] == 'R'): 
                return False
        return True


    def solution2and3(self,start, end):
        '''
        Solution to problem 2 and problem 3
        Shortest Path from Start to End is given by the standard BFS routine
        
        Output
        Prints the shortest path from start square to end square 

        Input 
        start :  Staring Knight Position in [row,col]
        end   :  Ending Knight Position in [row,col]

        

        '''
        visited = [[[-1, -1]] * self.w for _ in xrange(self.w)]
        q = deque([])
        q.append(start)
        visited[start[0]][start[1]] = start  # mark current node as visited

        while q and q[0] != end:

            node_r, node_c = q.popleft() 

            # Check for all possible 8 knight positions 
            moves =[(-1,-2),(1,2),(-1,2),(1,-2),(-2,-1),(2,1),(-2,1),(2,-1)]

            for i in xrange(8):
                if (self.is_valid_position([node_r + moves[i][0],node_c + moves[i][1]]) and 
                    visited[node_r + moves[i][0]][node_c + moves[i][1]] == [-1, -1]):

                    visited[node_r + moves[i][0]][node_c + moves[i][1]] = [node_r, node_c]
                    q.append([node_r + moves[i][0], node_c + moves[i][1]])



        shortest_path = []
        curr = end
        while(curr != start):
            shortest_path = [curr] + shortest_path
            curr = visited[curr[0]][curr[1]]
        
        # Include the starting position
        shortest_path = [start] + shortest_path  
        print shortest_path


    def is_valid_32(self,next_move, curr):
        '''
        For 32x32 board,
        Checks if the next_move is a valid move for a Knight
        Given that the curr is the current position of the Knight
        Checks for R[ock] and B[arrier] constraints

        Input
        next_move : Next move on board in [row,col]
        curr      : Current position of Knight in [row,col]
        '''
        if not self.is_valid_move(next_move, curr):
            # Check if the next_move is valid for a Knight 
            return False

        # Accomodate for R[ock] and B[arrier] squares

        # Can't land on rock or blocked
        if (self.board[next_move[0]][next_move[1]] == 'R'
            or self.board[next_move[0]][next_move[1]] == 'B'):  
            return False


        # down-left or down-right
        if (next_move[0] - curr[0] == 2 and
            abs(next_move[1] - curr[1]) == 1):
            return (self.board[curr[0] + 1][curr[1]] != 'B'and 
            self.board[curr[0] + 2][curr[1]] != 'B')

        # up-left or up-right
        if (next_move[0] - curr[0] == -2 and 
           abs(next_move[1] - curr[1])) == 1:
            return (self.board[curr[0] - 1][curr[1]] != 'B'and 
            self.board[curr[0] - 2][curr[1]] != 'B')

        # left-up or left-down
        if (abs(next_move[0] - curr[0]) == 1 and
            next_move[1] - curr[1] == -2):
            return (self.board[curr[0]][curr[1] - 1] != 'B'and 
            self.board[curr[0]][curr[1] - 2] != 'B')
        # right-up or right-down
        if (abs(next_move[0] - curr[0]) == 1 and
            next_move[1] - curr[1]) == 2:
            return (self.board[curr[0]][curr[1] + 1] != 'B'and
            self.board[curr[0]][curr[1] + 2] != 'B')


    def move_cost(self,next_move):
        '''
        Returns cost of making the move factoring in cost for W[ater] 
        and R[ock] for 32x32 board 

        Input
        next_move : Next move on board in [row,col]
        '''
        if self.board[next_move[0]][next_move[1]] == 'W':
            return 2
        if self.board[next_move[0]][next_move[1]] == 'L':
            return 5
        return 1

    def solution4(self,start, end):
        '''
        Implementing Dijkstra's algorithm with Greedy approach

        Pseudocode
        seen=set()
        q=[(0,start,tuple(start))] #cost,current_node,path to current node

        while q:
            (path_cost,v,path)=heapq.heappop(q) # Pop out closest element
            if v not in seen:
                seen.add(v)
                if v==end:   	# found target
                    return (c,p)

                for edge_cost,u in neighbours(v): # implemented with 32*32 board constraints
                    if u not in seen:
                        heapq.heappush(q,(edge_cost+path_cost,u,path+tuple([u])))

        Input 
        start :  Staring Knight Position in [row,col]
        end   :  Ending Knight Position in [row,col]


        '''


        seen = [[0] * 32 for _ in xrange(32)] 
        q = [(0, start, tuple([start]))]  # Adding start node to queue with cost=0

        while q:
            # Select the node with closest distance
            d_node, [node_r, node_c], path = heapq.heappop(q)  
            if not seen[node_r][node_c]:
                # Mark current node as seen
                seen[node_r][node_c] = 1

                if [node_r, node_c] == end: # Found the target node
                    return d_node, path

                # Accomodate for T[eleport] square
                if [node_r, node_c] == [11, 26] and not seen[23][27]:  
                    heapq.heappush(q, (d_node + 0, [
                        23, 27], path + tuple([[23, 27]]))) # Zero Cost
                    continue # Skip the iteration

                # Accomodate for other T[eleport] square
                if [node_r, node_c] == [23, 27] and not seen[11][26]:   
                    heapq.heappush(q, (d_node + 0,
                        [11, 26], path + tuple([[11, 26]]))) # Zero Cost
                    continue

                moves = [(-1,-2),(1,2),(-1,2),(1,-2),(-2,-1),(2,1),(-2,1),(2,-1)]

                # Checking for all 8 Knight moves
                # Nodes are added if the move is valid AND
                # They are NOT already marked seen
                for i in xrange(8):

                    if (self.is_valid_32([node_r + moves[i][0], node_c + moves[i][1]],
                        [node_r, node_c]) and not 
                        seen[node_r + moves[i][0]][node_c + moves[i][1]]):

                        heapq.heappush(q, (
                            self.move_cost([node_r + moves[i][0], node_c + moves[i][1]]) + d_node, 
                            [node_r + moves[i][0], node_c + moves[i][1]],
                            path + tuple([[node_r + moves[i][0], node_c + moves[i][1]]])))


# def updateCurrentPosition(next_move, curr):
#     '''
#     Return next_move if it is valid for given current move
#     Valid for both 8x8 and 32x32 boards
#     '''
#     # do not move the rook if the move is invalid
#     if not is_valid_32(next_move,curr):  
#         return curr
#     # T[eleport] square
#     elif next_move == [11, 26]:  
#         return [23, 27]  # Other T[eleport] square

#     elif next_move == [23, 27]:  # T[eleport] square
#         return [11, 26]  # Other T[eleport] square
#     else:
#         return next_move

def longestSequence(curr,path_len):
    #print curr,is_valid_32Position(curr)
    
          
    if seq32[curr[0]][curr[1]]>0:
        #print curr,'here',path_len
        return False # used square
    
    seq32[curr[0]][curr[1]]= path_len
    path_len+= 1
    if path_len == 63:
            return True

    
    moves = [(-1,-2),(1,2),(-1,2),(1,-2),(-2,-1),(2,1),(-2,1),(2,-1)]
    
    for i in xrange(8):
        if (is_valid_move([curr[0] + moves[i][0],curr[1] + moves[i][1]],
                      [curr[0], curr[1]]) and  
                    longestSequence([curr[0] + moves[i][0],curr[1] + moves[i][1]],path_len)):
                        return True
#        if (is_valid_32([curr[0] + moves[i][0], curr[1] + moves[i][1]],
#                      [curr[0], curr[1]]) and  
#                    longestSequence([curr[0] + moves[i][0],curr[1] + moves[i][1]],path_len)):
#                    return True
    
    
    seq32[curr[0]][curr[1]] = -1
    path_len-=1
    return False                  
                        
   

    
    

if __name__ == "__main__":
    board8=Solution(8)
    
    print 'Level 1'
    
    start = input('Enter starting position in [row,col] - ')
    while not board8.is_valid_position(start):
       start = input ('Enter a valid starting position in [row,col] - ')

    board8.print_curr_board(start)
    curr = start
    next_move = input ('Enter a move in [row,col] for Bishop. Enter "Q" to exit Level 1 - ')

    while next_move != 'Q':
        if board8.is_valid_move(next_move,curr):
           curr = next_move
           board8.print_curr_board(curr)
        else:
           print '!------This move is not valid------!'
        next_move = input ('Enter a move in [row,col] for Bishop. Enter "Q" to exit Level 1 - ')

    print '\n'

    print 'Level 2 & Level 3'

    start = input('Enter starting position in [row,col] - ')
    while not board8.is_valid_position(start):
       start = input ('Enter a valid starting position in [row,col] - ')

    end = input('Enter ending position in [row,col] - ')
    while not board8.is_valid_position(end):
       end = input ('Enter a valid ending position in [row,col] - ')
    
    board8.solution2and3(start,end)

    print 'Level 4'

    board32 = Solution(32)
    start = input('Enter starting position in [row,col] - ')
    while not board32.is_valid_position(start):
       start = input ('Enter a valid starting position in [row,col] - ')

    end = input('Enter ending position in [row,col] - ')
    while not board32.is_valid_position(end):
       end = input ('Enter a valid ending position in [row,col] - ')

    print  board32.solution4(start,end)

    # print 'Level 5'

