# dApp لإرسال واستقبال ETH

هذا تطبيق لامركزي بسيط يستخدم Ethereum لإرسال واستقبال ETH عبر العقد الذكي باستخدام Solidity وواجهة HTML + JavaScript.

## كيفية التشغيل:

1. قم بتثبيت الحزم:
   ```bash
   npm install
git init
git remote add origin https://github.com/اسم_المستخدم/eth-dapp-send-receive.git
git add .
git commit -m "Initial commit"
git push -u origin main
cd frontend
python -m http.server 8000
npx hardhat run scripts/deploy.js --network localhost
npx hardhat node
<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <title>إرسال واستقبال ETH</title>
</head>
<body>
    <h1>تطبيق إرسال واستقبال ETH</h1>
    <input type="text" id="address" placeholder="عنوان المستلم">
    <input type="number" id="amount" placeholder="المبلغ بالـ ETH">
    <button id="send">إرسال</button>

    <script src="https://cdn.jsdelivr.net/npm/ethers/dist/ethers.min.js"></script>
    <script>
        const provider = new ethers.providers.Web3Provider(window.ethereum);
        let signer;
        let contract;

        async function init() {
            await provider.send("eth_requestAccounts", []);
            signer = provider.getSigner();
            const contractAddress = "عنوان_العقد_الذكي";
            const abi = [/* ABI الخاص بالعقد الذكي */];
            contract = new ethers.Contract(contractAddress, abi, signer);
        }

        document.getElementById("send").onclick = async () => {
            const address = document.getElementById("address").value;
            const amount = document.getElementById("amount").value;
            const tx = await contract.send(address, { value: ethers.utils.parseEther(amount) });
            await tx.wait();
            alert("تم الإرسال بنجاح!");
        };

        init();
    </script>
</body>
</html>
