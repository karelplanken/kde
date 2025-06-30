<a href="../README.md">Back to README</a>

# Collection of Tools for Ubuntu

In these install instruction you will find a how to install a couple of tool I use in my development setup. The tools listed here did not fit anywhere else and in this way it is just a list of, what I consider optional tools, except for the SQLite interface.

## SQLite

### What is SQLite?

[SQLite](https://sqlite.org/index.html) is a lightweight, self-contained, and serverless SQL database engine. Unlike traditional database systems like MySQL or PostgreSQL, SQLite is not a separate server process, it is a C library that applications embed directly. The entire database is stored in a single file on disk.

### Why Use SQLite?

- Zero configuration: No setup or server management required.
- Portable: The database is a single file that can be easily copied or shared.
- Reliable: Fully ACID-compliant with support for transactions.
- Fast and efficient: Ideal for small to medium-sized applications.
- Cross-platform: Works on Linux, Windows, macOS, and more.

### Where is SQLite Used?

- Mobile apps (e.g., Android, iOS)
- Embedded systems (e.g., IoT devices, firmware)
- Desktop applications (e.g., browsers like Firefox)
- Testing and prototyping (quick setup without a full DBMS)
- Data storage for small tools and scripts

### Install sqlite3 on Ubuntu

To work with SQLite databases directly, we need to install an SQLite interface on Linux.

1. To install the SQLite command-line interface on Ubuntu, first update your package list:

    ```bash
    sudo apt update
    ```

2. Because sqlite3 is frequently pre-installed, check if you already have it on your system:

    ```bash
    sqlite3 --version
    ```

    If you don't see a version number, SQLite is likely not installed, proceed to the next step. If it is installed, you can try to update it via:

    ```bash
    sudo apt install sqlite3 --only-upgrade
    ```

3. Then install the interface:

    ```bash
    sudo apt install sqlite3
    ```

4. Verify the installation by checking the version of sqlite3: 

    ```bash
    sqlite3 --version
    ```

## Fastfetch

### What is Fastfetch?

[Fastfetch](https://github.com/fastfetch-cli/fastfetch) is a fast and highly customizable system information tool, similar to Neofetch, but written primarily in C for better performance. It fetches and displays system details—like OS, kernel, uptime, CPU, GPU, memory, and more—in a visually appealing format, often alongside your system logo in ASCII or image form.

Fastfetch is designed to be:
- Lightweight: Minimal dependencies and fast execution.
- Modular: Output can be customized extensively via command-line options or configuration files.
- Scriptable: Ideal for use in shell scripts, status bars, or terminal dashboards.

### Why Use Fastfetch?

- Performance: Written in C, it runs faster than many alternatives.
- Customizability: Output format, colors, logos, and modules can be tailored to your preferences.
- Modern features: Supports image logos, JSON output, and more. Perfect for showing off your system setup.

### Install Fastfetch on Ubuntu

To install Fastfetch on Ubuntu, you can use a community-maintained PPA:

1. Add the Fastfetch PPA:

    ```bash
    sudo apt-add-repository ppa:zhangsongcui3371/fastfetch
    ```

2. Update your package list:

    ```bash
    sudo apt update
    ```

3. Install Fastfetch:

    ```bash
    sudo apt install fastfetch
    ```

4. Now you can obtain system information very fast by running Fastfetch:

    ```bash
    fastfetch
    ```

## CMatrix

CMatrix is based on the screensaver from *The Matrix* website. It shows text flying in and out of the terminal, just like in the iconic scenes from *The Matrix* movie. Since I'm a fan of the Matrix Trilogy, it's a must-have for me.

### Install CMatrix

```bash
sudo apt install cmatrix
```

Run it with:

```bash
cmatrix
```

## Fortune

For daily wisdom, I use Fortune, the haiku sans cookie. It prints a random quote, joke, or proverb each time you run it...

### Install Fortune

Install Fortune:

```bash
sudo apt install fortune
```

Run it with:

```bash
fortune
```

## Cowsay

[Cowsay](https://web.archive.org/web/20120319053732/http://linuxgazette.net/issue67/orr.html) is a program that generates ASCII art of a cow (or other characters) saying something. It’s quirky, fun, and perfect for injecting a little humor into your terminal. I sometimes use it just to trigger a smile.

## Install Cowsay

Install Cowsay:

```bash
sudo apt install cowsay
```

Run Fortune:

```bash
cowsay "hello, world"
```

### Combine Cowsay and Fortune

IMHO, this is most fun combo:

```bash
fortune | cowsay -f tux
```

Tip: You can explore other characters with cowsay -l

<a href="../README.md">Back to README</a>