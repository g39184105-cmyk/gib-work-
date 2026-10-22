# gib-work-
import "dotenv/config";
import { createGibworkClient } from "@gibwork/sdk/node";

async function main() {
  const privateKey = process.env.SOLANA_PRIVATE_KEY;

  if (!privateKey) {
    throw new Error(
      "SOLANA_PRIVATE_KEY ortam değişkeni bulunamadı."
    );
  }

  const gibwork = createGibworkClient({
    privateKey,
    production: true,
  });

  // Gibwork üzerindeki kullanılabilir görevleri getir.
  const tasks = await gibwork.tasks.listAvailable({
    page: 1,
    limit: 15,
  });

  console.log("GIBWORK GÖREVLERİ");
  console.log("=================");

  console.log(JSON.stringify(tasks, null, 2));
}

main().catch((error) => {
  console.error("Hata:", error);
  process.exitCode = 1;
});