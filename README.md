from random import shuffle

class Carta:
    valores = ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']
    naipes = ['Copas', 'Ouros', 'Paus', 'Espadas']
    def __init__(self, valor, naipe):
        self.valor = valor
        self.naipe = naipe
    def __lt__(self, other):
        if Carta.naipes.index(self.naipe) == Carta.naipes.index(other.naipe):
            return Carta.valores.index(self.valor) < Carta.valores.index(other.valor)
        else:
            return Carta.naipes.index(self.naipe) < Carta.naipes.index(other.naipe)
    def __gt__(self, other):
        if Carta.naipes.index(self.naipe) == Carta.naipes.index(other.naipe):
            return Carta.valores.index(self.valor) > Carta.valores.index(other.valor)
        else:
            return Carta.naipes.index(self.naipe) > Carta.naipes.index(other.naipe)
    def __str__(self):
        return f"{self.valor} de {self.naipe}"
       
class Baralho:
    def __init__(self):
        self.cartas = [Carta(valor, naipe) for valor in Carta.valores for naipe in Carta.naipes]
    def embaralhar(self):
        shuffle(self.cartas)
    def retirar_carta(self):
        print("Retirando uma carta do baralho...")
        return self.cartas.pop(0)
    def organizar(self):
        self.cartas.sort()

def blackjack():
    baralho = Baralho()
    jogador_hand = []
    dealer_hand = []
    jogador_points = 0
    dealer_points = 0

    print("Bem-vindo ao jogo de Blackjack!")
    baralho.embaralhar()
    print("O baralho foi embaralhado. Vamos começar o jogo!")
    #distribuir as cartas iniciais para o jogador e o dealer
    for c in range(2):
        jogador_hand.append(baralho.retirar_carta())
        dealer_hand.append(baralho.retirar_carta())
    #mostrar as cartas do jogador e a primeira carta do dealer
    print("="*50)
    print("Distribuindo as cartas iniciais...")
    print("Cartas distribuídas!")
    print(f"Cartas do dealer: {dealer_hand[0]} e uma carta oculta")
    print(f"Suas cartas: {jogador_hand[0]} e {jogador_hand[1]}")
    print("="*50)
    #calcular os pontos iniciais do jogador e do dealer
    jogador_points = sum(10 if carta.valor in ['10', 'J', 'Q', 'K'] else 11 if carta.valor == 'A' else int(carta.valor) for carta in jogador_hand)
    dealer_points = 10 if dealer_hand[0].valor in ['10', 'J', 'Q', 'K'] else 11 if dealer_hand[0].valor == 'A' else int(dealer_hand[0].valor)
    print(f"Total de pontos do jogador: {jogador_points}")
    print(f"Total de pontos do dealer: {dealer_points}")
    dealer_points = sum(10 if carta.valor in ['10', 'J', 'Q', 'K'] else 11 if carta.valor == 'A' else int(carta.valor) for carta in dealer_hand)

    #verificar se o jogador ou o dealer tem Blackjack
    if jogador_points == 21 and dealer_points == 21:
        print(f"Total de pontos do jogador: {jogador_points}")
        print(f"Total de pontos do dealer: {dealer_points}")
        print("Empate! Ambos têm Blackjack!")
        return
    
    elif jogador_points == 21 and dealer_points != 21:
        print(f"Total de pontos do jogador: {jogador_points}")
        print(f"Total de pontos do dealer: {dealer_points}")
        print("Parabéns! Você tem Blackjack e venceu!")
        return
    
    else:
        while True:
            #perguntar ao jogador se ele deseja 'HIT' ou 'STAND'
            escolha = input("Deseja 'HIT' para pedir mais cartas ou 'STAND' para ficar com as cartas que ja possui? ").upper()
            if escolha == 'HIT':
                #adicionar uma carta à mão do jogador
                jogador_hand.append(baralho.retirar_carta())
                #atualizar os pontos do jogador
                if jogador_hand[-1].valor in ['10', 'J', 'Q', 'K']:
                    jogador_points += 10

                elif jogador_hand[-1].valor == 'A' and jogador_points + 11 <= 21:
                    jogador_points += 11

                elif jogador_hand[-1].valor == 'A' and jogador_points + 11 > 21:
                    jogador_points += 1

                else:
                    jogador_points += int(jogador_hand[-1].valor)
                    #mostra as cartas do jogador e os pontos atuais
                print(f"Suas cartas: [{ ', '.join(str(c) for c in jogador_hand)}] - Total de pontos: {jogador_points}")

                #verificar se o jogador estourou ou se tem Blackjack
                if jogador_points > 21:
                    print("Você estourou! Você perdeu!")
                    return
                
                if jogador_points == 21 and dealer_points == 21:
                        print(f"Total de pontos do jogador: {jogador_points}")
                        print(f"Total de pontos do dealer: {dealer_points}")
                        print("Empate! Ambos têm Blackjack!")
                        break
                        
            elif escolha == 'STAND':
                    print(f"Você escolheu STAND. Suas cartas finais: [{ ', '.join(str(c) for c in jogador_hand)}] - Total de pontos: {jogador_points}")
                    print(f"Cartas do dealer: [{ ', '.join(str(c) for c in dealer_hand)}] - Total de pontos: {dealer_points}")
                    break
            else:
                print("Opção inválida. Por favor, escolha 'HIT' ou 'STAND'.")
                break
            #dealer joga
        while dealer_points < 17:
            dealer_hand.append(baralho.retirar_carta())
                    
                #atualizar os pontos do dealer
            if dealer_hand[-1].valor in ['10', 'J', 'Q', 'K']:
                dealer_points += 10

            elif dealer_hand[-1].valor == 'A' and dealer_points + 11 <= 21:
                dealer_points += 11

            elif dealer_hand[-1].valor == 'A' and dealer_points + 11 > 21:
                dealer_points += 1

            else:
                dealer_points += int(dealer_hand[-1].valor)
                #mostrar as cartas do dealer e os pontos atuais
            print(f"Cartas do dealer: [{ ', '.join(str(c) for c in dealer_hand)}] - Total de pontos: {dealer_points}")

                #verificar se o dealer estourou ou se tem Blackjack
        if dealer_points == jogador_points == 21:
            print(f"Total pontos do dealer: {dealer_points}")
            print(f"Total pontos do jogador: {jogador_points}")
            print("Empate! Ambos têm Blackjack!")

        elif dealer_points == 21:
            print(f"Total pontos do dealer: {dealer_points}")
            print(f"Total pontos do jogador: {jogador_points}")
            print("O dealer tem Blackjack! Você perdeu!")

        elif dealer_points > 21:
            print(f"Total pontos do dealer: {dealer_points}")
            print(f"Total pontos do jogador: {jogador_points}")
            print("O dealer estourou! Parabéns, você venceu!")
                    

        elif dealer_points < jogador_points:
            print(f"Total pontos do dealer: {dealer_points}")
            print(f"Total pontos do jogador: {jogador_points}")
            print("Parabéns! Você venceu!")
                    

        elif dealer_points > jogador_points:
            print(f"Total pontos do dealer: {dealer_points}")
            print(f"Total pontos do jogador: {jogador_points}")
            print("O dealer venceu! Você perdeu!")
                      

                
blackjack()
    
