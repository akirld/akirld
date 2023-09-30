
import random


# カードをデッキからランダムに1枚取得する関数
def deal_card(deck):
    return random.choice(deck)


# 手札の点数を計算する関数（Acesの値を考慮）
def calculate_score(hand):
    score = sum(hand)
    if 11 in hand and score > 21:
        hand.remove(11)
        hand.append(1)
        score = sum(hand)
    return score


# ブラックジャックゲームのメイン関数
def blackjack():
    # カードデッキを定義
    cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
    my_hand = []  # プレイヤーの手札
    dealer_hand = []  # ディーラーの手札


    # 初期の手札を2枚ずつ配る
    for _ in range(2):
        my_hand.append(deal_card(cards))
        dealer_hand.append(deal_card(cards))


    game_over = False


    while not game_over:
        my_score = calculate_score(my_hand)
        dealer_score = calculate_score(dealer_hand)


        print(f"自分のカード: {my_hand}, 現在のスコア: {my_score}")
        print(f"ディーラーの最初のカード: {dealer_hand[0]}")


        if my_score == 0 or dealer_score == 0 or my_score > 21:
            game_over = True
        else:
            ans = input("もう1枚カードを引きますか？ 'yes' または 'no' で答えてください: ").lower()
            if ans == "yes":
                my_hand.append(deal_card(cards))
            else:
                game_over = True


    while dealer_score < 17:
        dealer_hand.append(deal_card(cards))
        dealer_score = calculate_score(dealer_hand)


    print(f"自分の最終手札: {my_hand}, 最終スコア: {my_score}")
    print(f"ディーラーの最終手札: {dealer_hand}, 最終スコア: {dealer_score}")
    print(compare_scores(my_score, dealer_score))


# スコアを比較して結果を返す関数
def compare_scores(player_score, dealer_score):
    if player_score > 21:
        return "バーストしてしまいました。あなたの負けです！"
    elif dealer_score > 21:
        return "ディーラーがバーストしました。あなたの勝ちです！"
    elif player_score == dealer_score:
        return "引き分けです！"
    elif player_score == 21:
        return "ブラックジャック！ あなたの勝ちです！"
    elif dealer_score == 21:
        return "ディーラーがブラックジャックを持ちました。あなたの負けです！"
    elif player_score > dealer_score:
        return "あなたの勝ちです！"
    else:
        return "あなたの負けです！"


if __name__ == "__main__":
    blackjack()

