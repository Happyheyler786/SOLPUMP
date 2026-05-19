# SOLPUMP
import { createHmac } from "crypto";

const serverSeed = "REVEALED_SERVER_SEED";
const clientSeed = "430605a44e44c9dda63e163664d515c96b9a0";

const saltedSeed = createHmac("sha256", serverSeed).update(clientSeed).digest("hex");
if (isDivisible(saltedSeed, 20)) return 1.00;
const h = parseInt(saltedSeed.slice(0, 13), 16);
const e = Math.pow(2, 52);
const crashPoint = Math.floor((100 * e - h) / (e - h)) / 100;

console.log("Crash Point:", crashPoint);

function isDivisible(hash, mod) {
  return BigInt("0x" + hash) % BigInt(mod) === 0n;
}