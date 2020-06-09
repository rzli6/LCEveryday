# 1169. Invalid Transactions

2020/06/09 ZLY

### Problem Description

- A transaction is *possibly invalid* if:

  - the amount exceeds $1000, or;
  - if it occurs within (and including) 60 minutes of another transaction with the same name in a different city.

  Each transaction string `transactions[i]` consists of comma separated values representing the name, time (in minutes), amount, and city of the transaction.

  Given a list of `transactions`, return a list of transactions that are possibly invalid. You may return the answer in any order.



### Algorithm

Use a dictionary to store all records with respect to the name. And we search the records under each person.

We use `set()` to store the results since there may be some duplicates.



### Code

```python
def invalidTransactions(self, transactions: List[str]) -> List[str]:
    record = collections.defaultdict(list)
    for transaction in transactions:
        name,time,amount,city = transaction.split(",")
        record[name].append([name,int(time),int(amount),city])
    def convert(s):
        return s[0]+","+str(s[1])+","+str(s[2])+","+s[3]
    result = set()
    for name, rec in record.items():
        curRec = sorted(rec,key = lambda x:x[1])
        for i in range(len(curRec)):
            if curRec[i][2]>1000:
                result.add(convert(curRec[i]))
            for j in range(i+1,len(curRec)):
                if curRec[j][1]-curRec[i][1] > 60:
                    break
                if curRec[j][3] != curRec[i][3]:
                    result.add(convert(curRec[i]))
                    result.add(convert(curRec[j]))
    return result
```