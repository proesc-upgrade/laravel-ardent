# Guia de Atualização para Laravel 5.0

Este documento descreve as mudanças feitas para atualizar o pacote Ardent do Laravel 4.2 para Laravel 5.0.

## Mudanças Realizadas

### 1. Dependências do Composer
Atualizadas todas as dependências do Illuminate de `~5.1` para `~5.0`:
- `illuminate/support`
- `illuminate/database`
- `illuminate/validation`
- `illuminate/events`
- `illuminate/hashing`

### 2. Estabilidade
Removida a configuração `"minimum-stability": "dev"` para melhor estabilidade em produção.

### 3. Documentação
- Atualizado o README.md para refletir suporte ao Laravel 5.0
- Atualizado o CHANGELOG.md com as mudanças realizadas
- Atualizada a descrição no composer.json

## Compatibilidade

### Laravel 5.0
✅ **Totalmente compatível** - Todas as funcionalidades do Ardent agora funcionam perfeitamente com Laravel 5.0.

### Laravel 4.2
⚠️ **Não é mais compatível** - Esta versão foi especificamente atualizada para Laravel 5.0 e não manterá compatibilidade retroativa com Laravel 4.2.

## Como Instalar

### Novo Projeto

Adicione ao seu `composer.json`:

```json
{
    "require": {
        "laravel-ardent/ardent": "~3.0"
    }
}
```

Execute:
```bash
composer update
```

### Projeto Existente (Migrando do Laravel 4.2)

1. Atualize seu Laravel para a versão 5.0
2. Atualize o composer.json do seu projeto conforme acima
3. Execute `composer update`

## Funcionalidades Mantidas

Todas as funcionalidades originais do Ardent foram mantidas:

- ✅ Auto-validação de modelos
- ✅ Validação customizada
- ✅ Model hooks (beforeSave, afterSave, etc.)
- ✅ Definição limpa de relacionamentos
- ✅ Auto-hidratação de entidades
- ✅ Purga automática de atributos redundantes
- ✅ Transformação automática de senhas (hashing)
- ✅ Suporte a regras unique em updates

## Código de Exemplo

```php
<?php

use LaravelArdent\Ardent\Ardent;

class User extends Ardent {
    
    public static $rules = array(
        'name'     => 'required|between:3,80|alpha_dash',
        'email'    => 'required|between:5,64|email|unique:users',
        'password' => 'required|min:6|confirmed',
        'password_confirmation' => 'required|min:6',
    );

    public static $passwordAttributes = array('password');
    public $autoHashPasswordAttributes = true;
    public $autoPurgeRedundantAttributes = true;
}

// Usar no seu controller
$user = new User();
$user->name = 'John Doe';
$user->email = 'john@example.com';
$user->password = 'secret123';
$user->password_confirmation = 'secret123';

if ($user->save()) {
    // Sucesso!
    echo "Usuário salvo com sucesso!";
} else {
    // Erros de validação
    $errors = $user->errors();
    foreach ($errors->all() as $error) {
        echo $error;
    }
}
```

## Notas Técnicas

### Facades Utilizadas
O pacote utiliza as seguintes facades do Laravel que são compatíveis com Laravel 5.0:
- `Input` - Para captura de dados de formulário
- `Hash` - Para hashing de senhas
- `Validator` - Para validação de dados

### Helper Functions
O pacote utiliza as seguintes helper functions que estão disponíveis no Laravel 5.0:
- `snake_case()`
- `camel_case()`

### Uso Standalone (Fora do Laravel)
O pacote ainda suporta uso fora do Laravel utilizando o método `configureAsExternal()`:

```php
\LaravelArdent\Ardent\Ardent::configureAsExternal(array(
    'driver'    => 'mysql',
    'host'      => 'localhost',
    'port'      => 3306,
    'database'  => 'my_database',
    'username'  => 'my_user',
    'password'  => 'my_password',
    'charset'   => 'utf8',
    'collation' => 'utf8_unicode_ci'
), 'pt-br'); // ou 'en' para inglês
```

## Suporte

Para reportar problemas ou contribuir com o projeto, visite:
- Issues: https://github.com/laravelbook/ardent/issues
- Documentação completa: Veja o README.md

## Créditos

- **Desenvolvedor Original**: Max Ehsan
- **Mantenedor Original**: Igor Santos
- **Atualização para Laravel 5.0**: Adaptado para compatibilidade com Laravel 5.0

## Licença

BSD-3-Clause (mantida do projeto original)

