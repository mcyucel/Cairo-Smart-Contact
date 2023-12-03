# Cairo-Smart-Contact
Cairo programlama dili ile akıllı sözleşme örneği
// Bu sözleşme, iki kullanıcı arasında bir para transferi gerçekleştirir.

struct Transfer {
    from: address,
    to: address,
    amount: u64,
}

// Sözleşmenin başlangıç fonksiyonudur.
public fun init() {
    // Sözleşmenin başlangıçta boş olduğunu doğrular.
    assert(transfers.length() == 0);
}

// Bir para transferi gerçekleştirir.
public fun transfer(from: address, to: address, amount: u64) {
    // Gönderenin hesabında yeterli para olduğundan emin olur.
    assert(balanceOf(from) >= amount);

    // Transferi kaydeder.
    transfers.push(Transfer(from, to, amount));

    // Gönderenin hesabından parayı çeker.
    balanceOf(from) -= amount;

    // Alıcının hesabına parayı yatırır.
    balanceOf(to) += amount;
}

// Transferleri döndürür.
public fun getTransfers(): vector<Transfer> {
    return transfers;
}

// Sözleşmenin ana veri yapısıdır.
private var transfers: vector<Transfer>;
