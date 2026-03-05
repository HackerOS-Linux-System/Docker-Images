# 1. Obraz bazowy
FROM debian:testing-slim

# 2. Definicja nazwy użytkownika (możesz ją zmienić przy budowaniu: --build-arg USERNAME=admin)
ARG USERNAME=forky
ENV HOME=/home/${USERNAME}

# 3. Instalacja niezbędnych narzędzi (curl do pobrania plików, ca-certificates dla HTTPS)
RUN apt-get update && apt-get install -y \
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# 4. Tworzenie użytkownika i struktury katalogów
RUN useradd -m -s /bin/bash ${USERNAME}
RUN mkdir -p ${HOME}/.hackeros/hacker-lang/bin/

# 5. Pobieranie binarek do katalogu domowego użytkownika
WORKDIR ${HOME}/.hackeros/hacker-lang/bin/
RUN curl -L -O https://github.com/HackerOS-Linux-System/Hacker-Lang/releases/download/v1.7.1/hl-runtime && \
    curl -L -O https://github.com/HackerOS-Linux-System/Hacker-Lang/releases/download/v1.7.1/hl-plsa && \
    curl -L -O https://github.com/HackerOS-Linux-System/Hacker-Lang/releases/download/v1.7.1/hl-compiler && \
    chmod +x *

# 6. Pobieranie głównej binarki do /usr/bin/
RUN curl -L -o /usr/bin/hl https://github.com/HackerOS-Linux-System/Hacker-Lang/releases/download/v1.7.1/hl && \
    chmod +x /usr/bin/hl

# 7. Ustawienie uprawnień dla całego katalogu domowego
RUN chown -R ${USERNAME}:${USERNAME} ${HOME}

# 8. Przełączenie na użytkownika
USER ${USERNAME}
WORKDIR ${HOME}

# 9. Dodanie binarek użytkownika do zmiennej PATH (opcjonalnie, dla wygody)
ENV PATH="${HOME}/.hackeros/hacker-lang/bin:${PATH}"

# Domyślne polecenie
CMD ["/bin/bash"]
