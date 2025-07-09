# Anotações Gerais sobre Criptografia

- [Introdução à Criptografia](#introdução-à-criptografia)
    - [O que é Criptografia?](#o-que-é-criptografia)
    - [Para que serve?](#para-que-serve)
    - [Como surgiu?](#como-surgiu)
    - [Como é usada hoje?](#como-é-usada-hoje)
- [Tipos de Criptografia](#tipos-de-criptografia)
    - [Criptografia Simétrica](#criptografia-simétrica)
    - [Criptografia Assimétrica](#criptografia-assimétrica)
    - [Criptografia Híbrida](#criptografia-híbrida)
- [Soluções e Algoritmos Mais Usados](#soluções-e-algoritmos-mais-usados)
    - [Simétricos](#simétricos)
    - [Assimétricos](#assimétricos)
    - [Assinaturas e Hashes](#assinaturas-e-hashes)
- [Alternativas e Comparações](#alternativas-e-comparações)
    - [Quando usar cada um?](#quando-usar-cada-um)
- [Conceitos Técnicos Fundamentais na Criptografia Simétrica](#conceitos-técnicos-fundamentais-na-criptografia-simétrica)
    - [Modos de Operação](#modos-de-operação)
    - [Padding](#padding-preenchimento)
    - [IV](#iv-initialization-vector---vetor-de-inicialização)
    - [Chave](#chave-key)
- [Exemplos Práticos em Java](#exemplos-práticos-em-java)
    - [Exemplo 1: Criptografia Simétrica com AES](#exemplo-1-criptografia-simétrica-com-aes)
    - [Exemplo 2: Criptografia Assimétrica com RSA](#exemplo-2-criptografia-assimétrica-com-rsa)
- [Considerações finais](#considerações-finais)

## Introdução à Criptografia

### O que é Criptografia?

- Criptografia é o processo de transformar informações legíveis (texto plano) em um formato ilegível (texto cifrado) com
  o
  objetivo de protegê-las contra acessos não autorizados. Ela garante que apenas quem possui a chave correta possa
  decifrar a informação e acessá-la em sua forma original.

### Para que serve?

- A criptografia é usada para:
    - **Confidencialidade**: proteger dados contra acessos não autorizados.
    - **Integridade**: garantir que os dados não foram alterados.
    - **Autenticidade**: validar a identidade do emissor.
    - **Não-repúdio**: impedir que o autor negue a autoria da informação.

### Como surgiu?

- A criptografia tem origem na antiguidade, usada por civilizações como Egito, Roma e Grécia. Um dos exemplos mais
  conhecidos é a **Cifra de César**, que deslocava letras do alfabeto para ocultar mensagens.
- Com o avanço da tecnologia, a criptografia evoluiu para algoritmos matemáticos complexos usados em sistemas digitais,
  comunicações online, bancos, governos, entre outros.

### Como é usada hoje?

- Comunicação segura na internet (HTTPS)
- Proteção de senhas e dados sensíveis em bancos de dados
- Autenticação de usuários e sistemas
- Assinaturas digitais
- Armazenamento seguro em dispositivos
- Criptomoedas e blockchain

## Tipos de Criptografia

### Criptografia Simétrica

- Usa a **mesma chave** para criptografar e descriptografar.
- Mais rápida e eficiente.
- Exige troca segura da chave entre as partes.
- Exemplos:
    - AES (Advanced Encryption Standard)
    - DES (Data Encryption Standard)

**Algoritmos comuns:**
| Algoritmo | Tamanho da chave | Observações |
|--------------|---------------------|----------------------------|
| AES | 128, 192, 256 bits | Algoritmo padrão moderno |
| Blowfish | 32–448 bits | Mais antigo, menos usado |
| DES / 3DES | 56 / 112 / 168 bits | Obsoleto, inseguro |
| ChaCha20 | 256 bits | Alternativa moderna ao AES |

### Criptografia Assimétrica

- Usa um **par de chaves**: uma pública e uma privada.
- A chave pública criptografa e a privada descriptografa (ou vice-versa).
- Mais segura para trocas de informação em redes inseguras.
- Exemplos:
    - RSA (Rivest–Shamir–Adleman)
    - ECC (Elliptic Curve Cryptography)
    - ElGamal

**Algoritmos comuns:**
| Algoritmo | Tamanho das chaves | Aplicações típicas |
|-----------|------------------------|------------------------------|
| RSA | 1024–4096 bits | Assinaturas, troca de chaves |
| EC (ECC)  | 256–521 bits | Alternativa mais leve ao RSA |
| ElGamal | Variável | Pouco usado atualmente |

### Criptografia Híbrida

- Combina os dois tipos: usa criptografia assimétrica para trocar a chave simétrica, e simétrica para os dados.
- Utilizada em protocolos como TLS/SSL (HTTPS).

## Soluções e Algoritmos Mais Usados

### Simétricos

- **AES**: padrão atual, forte e confiável.
- **ChaCha20**: alternativa moderna, eficiente em dispositivos móveis.

### Assimétricos

- **RSA**: clássico, amplamente usado.
- **ECDSA/ECDH**: baseado em curvas elípticas, menor chave com mesma segurança.

### Assinaturas e Hashes

- **SHA-256/SHA-3**: funções de hash para integridade.
- **HMAC**: hash autenticado.
- **JWT**: JSON Web Token para autenticação e troca segura de dados.

## Alternativas e Comparações

| Algoritmo | Tipo        | Vantagens                         | Desvantagens                        |
|-----------|-------------|-----------------------------------|-------------------------------------|
| AES       | Simétrico   | Rápido, confiável                 | Troca de chave pode ser um problema |
| RSA       | Assimétrico | Seguro para troca de chave        | Lento, chaves grandes               |
| ECC       | Assimétrico | Segurança com chaves menores      | Complexidade de implementação       |
| ChaCha20  | Simétrico   | Eficiência em dispositivos móveis | Menos padronizado                   |

### Quando usar cada um?

- **AES**: Para dados em repouso ou transferência entre partes com chave compartilhada.
- **RSA/ECC**: Para troca de chaves e assinatura digital.
- **Híbrido (TLS/SSL)**: Para comunicação segura na web.
- **Hash (SHA/HMAC)**: Para garantir integridade de dados.

## Conceitos Técnicos Fundamentais na Criptografia Simétrica

### Modos de Operação

Os algoritmos de criptografia simétrica como o **AES** operam em blocos fixos de dados (ex: 128 bits). Para lidar com
dados maiores que um bloco, usam-se os **modos de operação**, que determinam como os blocos são criptografados em
sequência.

#### Modos mais comuns:

| Modo | Nome                  | Características                                                                            |
|------|-----------------------|--------------------------------------------------------------------------------------------|
| ECB  | Electronic Codebook   | Cada bloco é criptografado isoladamente. Inseguro, pois blocos iguais geram saídas iguais. |
| CBC  | Cipher Block Chaining | Cada bloco é combinado com o anterior. Usa um IV único e aleatório. Mais seguro que ECB.   |
| CFB  | Cipher Feedback       | Transforma bloco em fluxo. Permite cifrar em unidades menores que o bloco.                 |
| OFB  | Output Feedback       | Similar ao CFB, mas independente do texto cifrado anterior.                                |
| CTR  | Counter               | Converte o bloco em fluxo com contador. Paralelizável e eficiente.                         |
| GCM  | Galois/Counter Mode   | Modo CTR com autenticação (confidencialidade + integridade). Muito usado em HTTPS.         |

### Padding (Preenchimento)

Os algoritmos de bloco exigem que o tamanho dos dados seja múltiplo do tamanho do bloco (ex: 128 bits = 16 bytes).
Quando não é, adiciona-se **padding** — dados extras — para completar o tamanho necessário.

#### Tipos de padding mais comuns:

| Tipo            | Descrição                                                                          |
|-----------------|------------------------------------------------------------------------------------|
| PKCS5Padding    | Preenche com N bytes, onde N é o número de bytes de preenchimento necessários.     |
| PKCS7Padding    | Idêntico ao PKCS5, mas funciona com qualquer tamanho de bloco.                     |
| NoPadding       | Nenhum padding é aplicado. Os dados devem ser múltiplos do tamanho do bloco.       |
| ISO10126Padding | Preenche com bytes aleatórios, exceto o último que indica o tamanho. (menos usado) |

### IV (Initialization Vector) - Vetor de Inicialização

O **vetor de inicialização (IV)** é um valor aleatório usado em alguns modos de operação (ex: CBC, CFB, OFB, GCM) para
garantir que o mesmo texto criptografado duas vezes com a mesma chave produza saídas diferentes.

- Deve ter o mesmo tamanho do bloco (ex: 16 bytes para AES).
- Não precisa ser secreto, mas **deve ser único e imprevisível**.
- Geralmente é transmitido junto com o texto cifrado para que a descriptografia seja possível.

### Chave (Key)

A chave é o segredo compartilhado usado para criptografar e descriptografar dados.

- Deve ter o comprimento correto (ex: 128, 192 ou 256 bits para AES).
- Nunca deve ser armazenada em texto plano.
- Pode ser derivada de senhas com algoritmos como PBKDF2, bcrypt, scrypt, ou Argon2.

**Exemplo de geração de chave AES em Java:**

```java
KeyGenerator keyGen = KeyGenerator.getInstance("AES");
keyGen.

init(256); // tamanho da chave em bits

SecretKey secretKey = keyGen.generateKey();
```

## Exemplos Práticos em Java

### Exemplo 1: Criptografia Simétrica com AES

A criptografia simétrica usa a mesma chave para criptografar e descriptografar dados. Um dos algoritmos mais comuns é o
AES (Advanced Encryption Standard).

#### Código exemplo

```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.IvParameterSpec;
import java.security.SecureRandom;
import java.util.Base64;

public class AESExample {

  /**
   * Gera uma chave secreta AES com 256 bits.
   * @return SecretKey para criptografia e descriptografia
   * @throws Exception
   */
  public static SecretKey generateAESKey() throws Exception {
    KeyGenerator keyGen = KeyGenerator.getInstance("AES");
    keyGen.init(256); // tamanho da chave em bits
    return keyGen.generateKey();
  }

  /**
   * Gera um vetor de inicialização (IV) de 16 bytes para AES.
   * @return IvParameterSpec contendo o IV
   */
  public static IvParameterSpec generateIV() {
    byte[] iv = new byte[16]; // AES bloco = 16 bytes
    new SecureRandom().nextBytes(iv); // gera bytes aleatórios
    return new IvParameterSpec(iv);
  }

  /**
   * Criptografa um texto usando AES/CBC/PKCS5Padding.
   * @param plaintext texto simples a ser criptografado
   * @param key chave secreta AES
   * @param iv vetor de inicialização
   * @return texto cifrado codificado em Base64
   * @throws Exception
   */
  public static String encrypt(String plaintext, SecretKey key, IvParameterSpec iv) throws Exception {
    Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding"); // modo CBC com padding PKCS5
    cipher.init(Cipher.ENCRYPT_MODE, key, iv);
    byte[] encrypted = cipher.doFinal(plaintext.getBytes("UTF-8"));
    return Base64.getEncoder().encodeToString(encrypted);
  }

  /**
   * Descriptografa um texto cifrado usando AES/CBC/PKCS5Padding.
   * @param ciphertext texto cifrado em Base64
   * @param key chave secreta AES
   * @param iv vetor de inicialização usado na criptografia
   * @return texto simples original
   * @throws Exception
   */
  public static String decrypt(String ciphertext, SecretKey key, IvParameterSpec iv) throws Exception {
    Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
    cipher.init(Cipher.DECRYPT_MODE, key, iv);
    byte[] decoded = Base64.getDecoder().decode(ciphertext);
    byte[] decrypted = cipher.doFinal(decoded);
    return new String(decrypted, "UTF-8");
  }

  public static void main(String[] args) {
    try {
      String originalText = "Olá, mundo! Este é um texto secreto.";

      // Gerar chave e IV
      SecretKey key = generateAESKey();
      IvParameterSpec iv = generateIV();

      System.out.println("Texto original: " + originalText);

      // Criptografar
      String encryptedText = encrypt(originalText, key, iv);
      System.out.println("Texto criptografado: " + encryptedText);

      // Descriptografar
      String decryptedText = decrypt(encryptedText, key, iv);
      System.out.println("Texto descriptografado: " + decryptedText);

    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

### Exemplo 2: Criptografia Assimétrica com RSA

Na criptografia assimétrica, há um par de chaves — uma pública para criptografar e uma privada para descriptografar. O
RSA é um dos algoritmos mais populares nesse modelo.

#### Código exemplo

```java
import java.security.KeyPair;
import java.security.KeyPairGenerator;
import java.security.PrivateKey;
import java.security.PublicKey;
import javax.crypto.Cipher;
import java.util.Base64;

public class RSAExample {

  /**
   * Gera um par de chaves RSA (pública e privada) de 2048 bits.
   * @return KeyPair contendo a chave pública e privada
   * @throws Exception
   */
  public static KeyPair generateKeyPair() throws Exception {
    KeyPairGenerator keyGen = KeyPairGenerator.getInstance("RSA");
    keyGen.initialize(2048); // tamanho da chave em bits
    return keyGen.generateKeyPair();
  }

  /**
   * Criptografa texto usando a chave pública RSA.
   * @param plaintext texto simples a ser criptografado
   * @param publicKey chave pública RSA
   * @return texto cifrado codificado em Base64
   * @throws Exception
   */
  public static String encrypt(String plaintext, PublicKey publicKey) throws Exception {
    Cipher cipher = Cipher.getInstance("RSA/ECB/OAEPWithSHA-256AndMGF1Padding");
    cipher.init(Cipher.ENCRYPT_MODE, publicKey);
    byte[] encrypted = cipher.doFinal(plaintext.getBytes("UTF-8"));
    return Base64.getEncoder().encodeToString(encrypted);
  }

  /**
   * Descriptografa texto cifrado usando a chave privada RSA.
   * @param ciphertext texto cifrado em Base64
   * @param privateKey chave privada RSA
   * @return texto simples original
   * @throws Exception
   */
  public static String decrypt(String ciphertext, PrivateKey privateKey) throws Exception {
    Cipher cipher = Cipher.getInstance("RSA/ECB/OAEPWithSHA-256AndMGF1Padding");
    cipher.init(Cipher.DECRYPT_MODE, privateKey);
    byte[] decoded = Base64.getDecoder().decode(ciphertext);
    byte[] decrypted = cipher.doFinal(decoded);
    return new String(decrypted, "UTF-8");
  }

  public static void main(String[] args) {
    try {
      String originalText = "Mensagem secreta para criptografia RSA";

      // Geração do par de chaves
      KeyPair keyPair = generateKeyPair();
      PublicKey publicKey = keyPair.getPublic();
      PrivateKey privateKey = keyPair.getPrivate();

      System.out.println("Texto original: " + originalText);

      // Criptografar com a chave pública
      String encryptedText = encrypt(originalText, publicKey);
      System.out.println("Texto criptografado: " + encryptedText);

      // Descriptografar com a chave privada
      String decryptedText = decrypt(encryptedText, privateKey);
      System.out.println("Texto descriptografado: " + decryptedText);

    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

## Considerações finais

- A criptografia simétrica é rápida e eficiente para grandes volumes de dados, mas requer que a chave seja compartilhada
  com segurança.
- A criptografia assimétrica facilita a troca segura de chaves e a autenticação, porém é mais lenta e indicada para
  pequenos volumes ou para proteger chaves simétricas.
- Na prática, sistemas seguros combinam ambos: usam RSA para proteger a chave AES e AES para criptografar os dados.