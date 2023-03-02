<script>
// @ts-nocheck

	import Prism from 'svelte-prism'

import { Tabs, TabList, TabPanel, Tab } from './tabs.js'


    let string =
  "010203040506070809101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293949596979899";
let pole = string.match(/..?/g);

let homophones = new Array();

let cislo = 99;
let rng;
let abc = "abcdefghijklmnopqrstuvwxyz";
let message = "Ahoj";
let encrypted = "";
for (let a = 0; a < 26; a++) {
  homophones.push([]);
  for (let b = 0; b < 3; b++) {
    rng = Math.floor(Math.random() * cislo);
    // @ts-ignore
    homophones[a].push(pole[rng]);
    // @ts-ignore
    pole.splice(rng, 1);
    cislo = cislo - 1;
  }
}
console.log(homophones);




function handleClick() {
encrypted = "";
  for (let i = 0; i < message.length; i++) {
    const letter = message[i].toLowerCase();
    if (letter !== " ") {

      const homophoneIndex = Math.floor(Math.random() * homophones[abc.indexOf(letter)].length);
      encrypted += homophones[abc.indexOf(letter)][homophoneIndex];
    } else {
      encrypted += message[i];
    }
  }
  
}

function handleClick2() {
  encrypted = '';
  for (let i = 0; i < (message.length + message.split(' ').length - 1)/2; i++) {
    const homophonesArray = Object.values(homophones).flat();
    console.log(homophonesArray)
    // @ts-ignore
    const homophoneIndex = homophonesArray.indexOf(message.match(/ |..?/g)[i]);
    if (homophoneIndex !== -1) {
      const letterIndex = Math.floor(homophoneIndex / 3);
      encrypted += abc[letterIndex];
    } else {
    
      encrypted += " ";
    }
    console.log(encrypted);
  }

}


</script>


    <link rel="stylesheet" href="/path/to/styles/default.min.css" />
    <div class="py-8">
        
        <h1 class="text-7xl pb-8 ">Homofonní Šifra</h1>
        <p class="text-l pb-8">
            Homofonní šifra patří mezi pokročilejší substituční šifry. Využívá nahrazování jednotlivých písmen abecedy za několik různých symbolů nebo kombinací symbolů. Tyto nahrazování jsou obvykle vytvořeny tak, aby každé písmeno mělo mnoho možných kombinací, a tím pádem je těžké zjistit, jaké písmeno nebo kombinace písmen daný symbol představuje. Homofonní šifry mohou být vytvářeny různými způsoby. Některé šifry nahrazují jednotlivá písmena za jediný symbol nebo kombinaci symbolů, zatímco jiné šifry používají různé symboly a kombinace pro každou jednotlivou pozici v textu. Tyto různé přístupy mají různé úrovně zabezpečení a složitosti. Pro vytvoření homofonní šifry je obvykle nutné mít klíč, který umožní převést šifrovaný text zpět do původního textu. Tento klíč obsahuje informace o tom, které symboly odpovídají jednotlivým písmenům abecedy. Bez klíče je dešifrování velmi obtížné a v některých případech nemožné.</p>
    <p></p>
    <label  for="text">Text k zašifrování</label>	
    <textarea
    class="block p-2.5 shadow appearance-none border rounded w-1/3	 py-2 my-5 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
    name="text"
    bind:value={message}
    />

<button
    class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
    on:click={handleClick}
    >
    Šifrovat
    </button>

    <button
    class="bg-transparent hover:bg-stone-900 text-stone-900 font-semibold hover:text-white py-2 px-4 border border-stone-900 hover:border-transparent rounded"
    on:click={handleClick2}
    >
    Dešifrovat
    </button>

    <h2 class="text-7xl pb-8 text-red-900">{encrypted}</h2>

    
    <Tabs>
        <TabList>
            <Tab>JS</Tab>
            <Tab>c#</Tab>
            <Tab>python</Tab>
        </TabList>
    
        <TabPanel>
        
            <Prism language="javascript">
                {`
    let cislo = 99;
    let rng;
    let abc = "abcdefghijklmnopqrstuvwxyz";
    let message = "Ahoj";
    let encrypted = "";
    for (let a = 0; a < 26; a++) {
    homophones.push([]);
    for (let b = 0; b < 3; b++) {
        rng = Math.floor(Math.random() * cislo);
        homophones[a].push(pole[rng]);
        pole.splice(rng, 1);
        cislo = cislo - 1;
    }
    }
    console.log(homophones);




    function encription() {
    encrypted = "";
    for (let i = 0; i < message.length; i++) {
        const letter = message[i].toLowerCase();
        if (letter !== " ") {

        const homophoneIndex = Math.floor(Math.random() * homophones[abc.indexOf(letter)].length);
        encrypted += homophones[abc.indexOf(letter)][homophoneIndex];
        } else {
        encrypted += message[i];
        }
    }
    
    }

    function decription() {
    encrypted = '';
    for (let i = 0; i < (message.length + message.split(' ').length - 1)/2; i++) {
        const homophonesArray = Object.values(homophones).flat();
        console.log(homophonesArray)
        const homophoneIndex = homophonesArray.indexOf(message.match(/ |..?/g)[i]);
        if (homophoneIndex !== -1) {
        const letterIndex = Math.floor(homophoneIndex / 3);
        encrypted += abc[letterIndex];
        } else {
        
        encrypted += " ";
        }
        console.log(encrypted);
    }

    } `}							
            </Prism>
    
        </TabPanel>
    
        <TabPanel>
            <Prism language="clike">
                {`
    using System;
    using System.Linq;
    
    namespace CaesarCipher
    {
    class Program
    {
        static void Main(string[] args)
        {
            Console.Write("Enter a message to encrypt: ");
            string message = Console.ReadLine();
    
            Console.Write("Enter a key (1-26): ");
            int key = int.Parse(Console.ReadLine());
    
            string encryptedMessage = Encrypt(message, key);
            Console.WriteLine($"Encrypted message: {encryptedMessage}");
    
            string decryptedMessage = Decrypt(encryptedMessage, key);
            Console.WriteLine($"Decrypted message: {decryptedMessage}");
        }
    
        static string Encrypt(string message, int key)
        {
            char[] encrypted = message.ToLower().ToCharArray().Select(c =>
            {
                if (!char.IsLetter(c))
                {
                    return c;
                }
    
                char letter = (char)(c + key);
    
                if (letter > 'z')
                {
                    return (char)(letter - 26);
                }
    
                return letter;
            }).ToArray();
    
            return new string(encrypted);
        }
    
        static string Decrypt(string message, int key)
        {
            return Encrypt(message, 26 - key);
        }
    }
    }
                `}							
            </Prism>
        </TabPanel>
        
        <TabPanel>
            <Prism language="clike">
                {`
    def cezar_cyper(plaintext, shift):
    cyphertext = ""
    for i in plaintext:
    if i.isalpha():
    cyphertext += chr((ord(i) - ord('a') + shift) % 26 + ord('a'))
    else:
    cyphertext += i
    return cyphertext
    
    print(cezar_cyper("hello world", 0)) # "khoor zruog"
    print(cezar_cyper("hello world", 7)) # "olssv dvysk"
    print(cezar_cyper("hello world", 11)) # "wrrrm jgtgt"
                `}							
            </Prism>
        </TabPanel>
    </Tabs>
    
    
    
    
    
    
    </div>
    <svelte:head>
        <link
            href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.22.0/themes/prism.min.css"
            rel="stylesheet"
        />
        
    </svelte:head>
    <style>
        label {
      color: black;
      font-weight: bold;
      display: block;
    }
    label:after { content: ": " }
    </style>