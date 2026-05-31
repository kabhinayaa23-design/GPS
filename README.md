class ExpenseSharing:
    def __init__(self, friends):
        self.friends = friends
        self.balances = {friend: 0 for friend in friends}

    def add_expense(self, payer, amount, participants):
        split_amount = amount / len(participants)
        for participant in participants:
            if participant != payer:
                self.balances[participant] -= split_amount
                self.balances[payer] += split_amount

    def calculate_settlement(self):
        print("\nFinal Settlement Report:")
        for friend, balance in self.balances.items():
            if balance > 0:
                print(f"{friend} needs to be reimbursed: Rs.{balance:.2f}")
            elif balance < 0:
                print(f"{friend} owes: Rs.{-balance:.2f}")
            else:
                print(f"{friend} is settled up.")

if __name__ == "__main__":
    friends = ["Abi", "Bala", "Creta"]
    expense_sharing = ExpenseSharing(friends)

    # Add some sample expenses
    expense_sharing.add_expense("Abi", 900, ["Abi", "Bala", "Creta"])
    expense_sharing.add_expense("Bala", 300, ["Abi", "Bala", "Creta"])
    expense_sharing.add_expense("Creta", 200, ["Abi", "Bala", "Creta"])

    # Calculate settlement
    expense_sharing.calculate_settlement()
