# Hello World - SUI Move Module

Smart contract sederhana untuk membuat dan mengelola greeting messages di SUI blockchain.

## 📋 Fitur Utama

- Membuat greeting object dengan custom message
- Update message (hanya creator)
- Read message dan creator info
- Event logging saat greeting dibuat

## 🏗️ Core Components

### Struct `Greeting`
```move
public struct Greeting has key, store {
    id: object::UID,     // Unique ID
    message: String,     // Pesan greeting
    creator: address,    // Pembuat greeting
}
```

### Event `GreetingCreated`
Emit event saat greeting baru dibuat dengan info ID, message, dan creator.

## 🚀 Functions

| Function | Description | Access |
|----------|-------------|---------|
| `create_greeting()` | Buat greeting baru + emit event | Public |
| `get_message()` | Baca message | Public (read-only) |
| `get_creator()` | Baca creator address | Public (read-only) |
| `update_message()` | Update message | Creator only |

## 💡 Key Concepts

- **Object Ownership**: Greeting dimiliki oleh creator
- **Access Control**: Hanya creator bisa update (`assert!` validation)
- **String Handling**: Input `vector<u8>` → UTF-8 string
- **Events**: Logging untuk off-chain monitoring
- **Error Handling**: Assert dengan error code untuk unauthorized access

## 💻 Usage Example

```bash
# Buat greeting
sui client call --function create_greeting --args "Hello SUI!"

# Baca message  
sui client call --function get_message --args [object-id]

# Update message (creator only)
sui client call --function update_message --args [object-id] "New message!"
```

## 🎯 Learning Points

- Basic Move syntax dan struct definition
- Owned objects dengan `key` ability  
- Simple authorization patterns
- Event emission
- UTF-8 string processing
- Test-only functions untuk development
