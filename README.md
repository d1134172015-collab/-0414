import random
import json
from datetime import datetime

class NumberLottery:
    def __init__(self):
        self.history = []

    def draw_numbers(self, start, end, count):
        if count > (end - start + 1):
            print("❌ 抽取數量超過範圍！")
            return
        
        numbers = list(range(start, end + 1))
        result = random.sample(numbers, count)
        result.sort()

        record = {
            "time": datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
            "range": f"{start}-{end}",
            "count": count,
            "result": result
        }

        self.history.append(record)

        print("\n🎉 抽獎結果：")
        print(result)

    def show_history(self):
        print("\n📜 抽獎紀錄：")
        for h in self.history:
            print(f"{h['time']} | 範圍:{h['range']} | 數量:{h['count']} → {h['result']}")

    def save_history(self):
        with open("number_lottery.json", "w", encoding="utf-8") as f:
            json.dump(self.history, f, ensure_ascii=False, indent=4)
        print("✅ 已儲存紀錄")

# ===== 主程式 =====
lottery = NumberLottery()

while True:
    print("\n=== 數字抽獎系統 ===")
    print("1. 抽數字")
    print("2. 查看紀錄")
    print("3. 儲存紀錄")
    print("4. 離開")

    choice = input("請選擇：")

    if choice == "1":
        start = int(input("起始數字："))
        end = int(input("結束數字："))
        count = int(input("抽幾個數字："))
        lottery.draw_numbers(start, end, count)

    elif choice == "2":
        lottery.show_history()

    elif choice == "3":
        lottery.save_history()

    elif choice == "4":
        break

    else:
        print("請輸入正確選項！")
