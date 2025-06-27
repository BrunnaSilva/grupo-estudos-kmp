# Kotlin Multiplatform - Projeto Exemplo Setup Inicial

> **Projeto do Grupo de Estudos KMP**
>
> Este é um projeto de exemplo para demonstrar o setup inicial de uma aplicação Kotlin Multiplatform (KMP) com Compose Multiplatform, desenvolvido para fins de estudo e aprendizado em grupo.

## 📱 Sobre o Projeto

Este projeto é um exemplo básico de **Kotlin Multiplatform** que demonstra:

- Compartilhamento de código entre Android e iOS
- Uso do **Compose Multiplatform** para UI compartilhada
- Estrutura de projeto recomendada para KMP
- Configuração de dependências e plugins

### Targets Suportados

- **Android** (API 24+)
- **iOS** (iOS 14+)

## 🛠️ Requisitos do Sistema

### Para Desenvolvimento Android

#### Requisitos Mínimos:

- **Java Development Kit (JDK)**: 11 ou superior
- **Android Studio**: Arctic Fox (2020.3.1) ou mais recente
- **Gradle**: 8.7+ (incluído no projeto)
- **Sistema Operacional**: Windows 10+, macOS 10.14+, ou Linux

#### Configuração do Android SDK:

- **Compile SDK**: 35
- **Target SDK**: 35
- **Min SDK**: 24
- **Android Gradle Plugin**: 8.7.3

### Para Desenvolvimento iOS (apenas macOS)

#### Requisitos Obrigatórios:

- **macOS**: 12.0 (Monterey) ou superior
- **Xcode**: 14.0 ou superior
- **iOS Simulator**: Incluído no Xcode
- **CocoaPods**: Para gerenciamento de dependências iOS

## 🚀 Setup do Ambiente

### 0. Instalação de Dependências (macOS/Linux)

Primeiro, instale o Homebrew se ainda não tiver:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Instale as dependências principais:

```bash

# Git (se não estiver instalado)
brew install git

# Para iOS development
brew install cocoapods
```

#### Via asdf (Gerenciador de Versões)

O asdf permite gerenciar múltiplas versões de diferentes ferramentas:

1. **Instale o asdf**:

   ```bash
   # Via Homebrew
   brew install asdf

   # Ou via Git
   git clone https://github.com/asdf-vm/asdf.git ~/.asdf --branch v0.14.0
   ```

2. **Configure o shell** (adicione ao seu `.bashrc`, `.zshrc`, etc.):

   ```bash
   # Para zsh
   echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ~/.zshrc

   # Para bash
   echo -e "\n. $(brew --prefix asdf)/libexec/asdf.sh" >> ~/.bashrc
   ```

3. **Instale os plugins necessários**:

   ```bash
   # Java
   asdf plugin add java
   ```

4. **Instale as versões específicas**:

   ```bash
   asdf install
   ```

5. **Verifique as instalações**:
   ```bash
   java -version
   ```

#### Configuração de Variáveis de Ambiente

Adicione ao seu arquivo de configuração do shell (`.zshrc`, `.bashrc`, etc.):

```bash
# Java Home (ajuste conforme sua instalação)
export JAVA_HOME=$HOME/.asdf/installs/java/openjdk-11.0.2
# Ou se instalado via brew:
# export JAVA_HOME=/opt/homebrew/opt/openjdk@11

# Android SDK (configure conforme sua instalação do Android Studio)
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools

# asdf
export PATH=$PATH:$HOME/.asdf/bin
```

Após adicionar, recarregue o terminal:

```bash
source ~/.zshrc  # ou ~/.bashrc
```

### 1. Clonagem do Repositório

```bash
git clone https://github.com/BrunnaSilva/grupo-estudos-kmp
cd projetos/exemplo-setup-inicial/KotlinProject
```

### 2. Configuração do Android Studio

1. **Abra o Android Studio**
2. **Importe o projeto**: `File > Open` → selecione a pasta do projeto
3. **Aguarde o sync inicial**: O Android Studio irá baixar as dependências automaticamente
4. **Configure o SDK**: Certifique-se de que o Android SDK 35 está instalado

### 3. Primeira Sincronização com Gradle

Após abrir o projeto no Android Studio:

1. **Sync automático**: O Android Studio iniciará automaticamente a sincronização
2. **Sync manual** (se necessário):
   ```bash
   ./gradlew build
   ```

### 4. Configuração para iOS (macOS apenas)

1. **Abra o Xcode**
2. **Instale as ferramentas de linha de comando**:
   ```bash
   xcode-select --install
   ```
3. **Navegue até a pasta iosApp**:
   ```bash
   cd iosApp
   ```

## 📁 Estrutura do Projeto

```
KotlinProject/
├── composeApp/                 # Módulo principal do app
│   ├── src/commonMain/         # Código compartilhado
│   ├── src/androidMain/        # Código específico Android
│   ├── src/iosMain/           # Código específico iOS
│   └── build.gradle.kts       # Configurações do módulo
├── iosApp/                    # Aplicação iOS nativa
│   ├── iosApp.xcodeproj/      # Projeto Xcode
│   └── Configuration/         # Configurações iOS
├── gradle/                    # Configurações Gradle
│   └── libs.versions.toml     # Catálogo de versões
├── build.gradle.kts          # Configuração raiz do projeto
└── settings.gradle.kts       # Configurações do projeto
```

### Pastas Importantes:

- **`/composeApp`**: Contém o código compartilhado da aplicação

  - `commonMain`: Código comum para todas as plataformas
  - `androidMain`: Código específico para Android
  - `iosMain`: Código específico para iOS
  - `commonTest`: Testes compartilhados

- **`/iosApp`**: Aplicação iOS nativa (ponto de entrada para iOS)

## ▶️ Executando o Projeto

### Android

#### Via Android Studio:

1. Abra o projeto no Android Studio
2. Aguarde o sync completar
3. Selecione o target `composeApp`
4. Clique em "Run" (▶️) ou pressione `Shift + F10`

#### Via Linha de Comando:

```bash
# Instalar no emulador/device
./gradlew installDebug

# Executar testes
./gradlew testDebug
```

### iOS (macOS apenas)

#### Via Android Studio:

1. Selecione o target iOS no Android Studio
2. Clique em "Run" para executar no simulador

#### Via Xcode:

1. Abra o arquivo `iosApp/iosApp.xcodeproj` no Xcode
2. Selecione um simulador ou device
3. Pressione `Cmd + R` para executar

#### Via Linha de Comando:

```bash
# Executar no simulador
./gradlew iosSimulatorArm64Run
```

## 🔧 Comandos Úteis

### Gradle Tasks Principais:

```bash
# Limpar build
./gradlew clean

# Build completo
./gradlew build

# Executar testes
./gradlew test

# Listar todas as tasks disponíveis
./gradlew tasks
```

### Troubleshooting Gradle:

```bash
# Limpar cache do Gradle
./gradlew clean --refresh-dependencies

# Verificar dependências
./gradlew dependencies
```

### Troubleshooting Ambiente:

```bash
# Verificar versões instaladas via asdf
asdf current

# Listar todas as versões disponíveis de uma ferramenta
asdf list all java
asdf list all kotlin
asdf list all gradle

# Reinstalar uma ferramenta via asdf
asdf uninstall java openjdk-11.0.2
asdf install java openjdk-11.0.2

# Verificar instalações via brew
brew list
brew doctor

# Atualizar ferramentas via brew
brew update
brew upgrade

# Verificar variáveis de ambiente importantes
echo $JAVA_HOME
echo $ANDROID_HOME
echo $PATH
```

## 📚 Tecnologias Utilizadas

- **Kotlin**: 2.1.21
- **Compose Multiplatform**: 1.8.1
- **Android Gradle Plugin**: 8.7.3
- **Gradle**: 8.7+
- **Target SDK**: Android 35, iOS 14+

## 🎯 Próximos Passos

Este projeto serve como base para:

1. Aprender conceitos de Kotlin Multiplatform
2. Experimentar com Compose Multiplatform
3. Entender compartilhamento de código
4. Praticar configurações de build
5. Explorar APIs específicas de cada plataforma

## 📖 Recursos Adicionais

- [Documentação Oficial Kotlin Multiplatform](https://kotlinlang.org/docs/multiplatform.html)
- [Compose Multiplatform](https://www.jetbrains.com/compose-multiplatform/)
- [Kotlin Multiplatform Samples](https://github.com/Kotlin/kmm-samples)
- [Guia Android Studio](https://developer.android.com/studio/intro)

## 🤝 Contribuindo

Este projeto faz parte do grupo de estudos. Sinta-se à vontade para:

- Fazer perguntas durante as sessões
- Sugerir melhorias
- Compartilhar descobertas
- Experimentar com novas funcionalidades

---

**Desenvolvido com ❤️ pelo Grupo de Estudos KMP**
