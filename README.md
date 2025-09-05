import random

TAMANHO = 5

def criar_tabuleiro():
    return [["~"] * TAMANHO for _ in range(TAMANHO)]

def mostrar_tabuleiro(tabuleiro):
    print("  " + " ".join([str(i) for i in range(TAMANHO)]))
    for i, linha in enumerate(tabuleiro):
        print(str(i) + " " + " ".join(linha))

def posicao_navio():
    linha = random.randint(0, TAMANHO-1)
    coluna = random.randint(0, TAMANHO-1)
    return linha, coluna

def jogar():
    tabuleiro = criar_tabuleiro()
    navio_linha, navio_coluna = posicao_navio()
    tentativas = 5

    print("=== BATALHA NAVAL ===")
    print(f"Tente acertar o navio escondido! Você tem {tentativas} tentativas.\n")
    
    while tentativas > 0:
        mostrar_tabuleiro(tabuleiro)
        try:
            palpite_linha = int(input("Escolha a linha (0-4): "))
            palpite_coluna = int(input("Escolha a coluna (0-4): "))
        except ValueError:
            print("Digite apenas números!")
            continue

        if (palpite_linha == navio_linha) and (palpite_coluna == navio_coluna):
            print("🎉 Parabéns! Você afundou o navio!")
            break
        else:
            if 0 <= palpite_linha < TAMANHO and 0 <= palpite_coluna < TAMANHO:
                if tabuleiro[palpite_linha][palpite_coluna] == "X":
                    print("Você já tentou essa posição!")
                else:
                    print("💦 Errou!")
                    tabuleiro[palpite_linha][palpite_coluna] = "X"
                    tentativas -= 1
            else:
                print("Fora do tabuleiro!")

        print(f"Tentativas restantes: {tentativas}\n")

    if tentativas == 0:
        print("❌ Suas tentativas acabaram!")
        print(f"O navio estava em ({navio_linha}, {navio_coluna})")

if __name__ == "__main__":
    jogar()
