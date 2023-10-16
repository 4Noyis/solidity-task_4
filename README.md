# solidity-task_4
Bu hafta ödevi derste anlattılan Token kontratının içerisinde bulunan Transfer metot ataklara karşı güvenli midir? Güvensizse nasıl bir revize yapmamız gerekir.

```bash
  function transfer(address to, uint256 amount) external {
        // Check if the transaction sender has enough tokens.
        // If `require`'s first argument evaluates to `false` then the
        // transaction will revert.
        require(balances[msg.sender] >= amount, "Not enough tokens");

        // Transfer the amount.
        balances[msg.sender] -= amount;
        balances[to] += amount;

        // Notify off-chain applications of the transfer.
        emit Transfer(msg.sender, to, amount);
    }
```

Öneri:
Bu işlev, yeterli bakiyeye sahip olmayan bir kullanıcı tarafından çağrılabilir. require kullanılmış gibi görünse de, bu kontrol işlemi sonrası gas ücreti ödenmiş olur ve ardından işlem geri alınır. Bu nedenle, kullanıcılar gas ücretini ödedikten sonra bakiyeyi kontrol etmek yerine, bu kontrolü işlem başlamadan önce yapmak daha güvenli olur.
