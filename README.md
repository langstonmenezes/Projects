# Projects
Solitaire Game
import random  # needed for shuffling a Deck

class Card():
    """Denote a card with rank and suit"""
    # Protocol:
    #   1. 'no card' is represented by BOTH r = 0 and s = ''
    #   2. set_rank and set_suit should be commented out after development and debugging
    #   3  rank is int: 1=Ace, 2-10 face value, 11=Jack, 12=Queen, 13=King
    def __init__(self, r=0, s=''): 
        self.__rank=0
        #self.__suit=''                 # create blank card by default unless we fix it later
        if type(r) == str:
            if r in 'Jj':
                self.__rank = 11  # Jack
            elif r in 'Qq':
                self.__rank = 12  # Queen
            elif r in 'Kk':
                self.__rank = 13  # King
            elif r in 'aA':
                self.__rank = 1   # Ace
            elif r=='2':
                self.__rank=2
            elif r=='3':
                self.__rank=3
            elif r=='4':
                self.__rank=4
            elif r=='5':
                self.__rank=5
            elif r=='6':
                self.__rank=6
            elif r=='7':
                self.__rank=7
            elif r=='8':
                self.__rank=8
            elif r=='9':
                self.__rank=9
            elif r=='10':
                self.__rank=10
        elif type(r) == int:
            if 1 <= r <= 14:
                self.__rank = r
    def get_rank(self):
        """Return rank of the card as int: 0-13"""
        return self.__rank
class Deck():
    """Denote a deck to play cards with"""
    
    def __init__(self,ftp):
        """Initialize deck as a list of all 52 cards: 13 cards in each of 4 suits"""
        self.__deck = [Card(j, i) for i in "CSHD" for j in range(1,14)] # list comprehension
        
    def shuffle(self):
        """Shuffle the deck"""
        random.shuffle(self.__deck) # random.shuffle() randomly rearranges a sequence

    def deal(self):
        """Deal a card by returning the card that is removed off the top of the deck"""
        if len(self.__deck) == 0:  # deck is empty
            return None
        else:
            return self.__deck.pop(0)  # remove card (pop it) and then return it
#####################################################################################################  
mydeck=['K','Q','J','A','2','3','4','5','6','7','8','9','10']#the entire deck 
mydeck=mydeck*4
random.shuffle(mydeck)#deck shuffled
deck=mydeck[0:52]
tab=deck[0:35]#the tableau
tab1=tab[0:5]#tableau divided into 7 rows with 5 cards each using slicing
tab2=tab[5:10]
tab3=tab[10:15]
tab4=tab[15:20]
tab5=tab[20:25]
tab6=tab[25:30]
tab7=tab[30:35]
stock=deck[35:51]
foundation=deck[51:52]


    
def remove(i):#function created to remove the cards based on which tab we select
    while True:
        i=i-1
        t=[tab1,tab2,tab3,tab4,tab5,tab6,tab7]
        k=t[i]#k becomes the selected tab
        
        x=Card(foundation[-1])  #check last index of the foundation
        x=x.get_rank()          #get the rank
        y=Card(k[-1])           #check last index of the foundation
        y=y.get_rank()          #get the rank
        
        if x==y+1 or x==y-1 or (x==13 and y==1) or (x==1 and y==13):#check if the card is in rank-1<rank<rank+1
            foundation.append(k[-1])#appends last index of tab selected to foundation
            k.pop(-1)#pops it
            k.insert(0,'')#replaces empty space to first index
        else:
            break
        
        for tabs in t:
            if tab[i]==[]:#if all the tabs are empty, the player wins
                print 'You Win!'
      
def play():
    while True:#We create this loop to create the layout of the game
        print '%5s %5s %5s %5s %5s %5s %5s'%('tab1','tab2','tab3','tab4','tab5','tab6','tab7')
        print '\n'
        i=0
        while i<5:
            print '%5s %5s %5s %5s %5s %5s %5s'%(tab1[i],tab2[i],tab3[i],tab4[i],tab5[i],tab6[i],tab7[i])
            i+=1
        print '\n'
        print 'stock',len(stock),foundation#prints the stock, its updated length whenever dealt and the foundation

        firstcard=raw_input('pick your tab: ')
            
        if firstcard.isdigit():
            firstcard=int(firstcard)
                
            if firstcard in range(1,8):#we have a range from 1-7 only. We select that which corresponds to the tab we select
                remove(firstcard)
            
        else:
            if firstcard in 'Dd':#D or d to deal a card from the stock
                foundation.append(stock[0])#appends the first index from stock to the foundation
                stock.pop(0)
            if firstcard in 'q':#to quit the game
                exit()
        if len(stock)==0:
            continue
    
play()#call the function to start playing the game

    
    
            
            
            

    
        
        
    
        








