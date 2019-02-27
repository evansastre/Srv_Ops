# encode&decode passwd string

```text
import base64
def encode(key, clear):
    enc = []
    for i in range(len(clear)):
        key_c = key[i % len(key)]
        enc_c = chr((ord(clear[i]) + ord(key_c)) % 256)
        enc.append(enc_c)
    return base64.urlsafe_b64encode("".join(enc))

def decode(key, enc):
    dec = []
    enc = base64.urlsafe_b64decode(enc)
    for i in range(len(enc)):
        key_c = key[i % len(key)]
        dec_c = chr((256 + ord(enc[i]) - ord(key_c)) % 256)
        dec.append(dec_c)
    return "".join(dec)


## This is an example, "decodekey", "Username", "Password" please refer to live environment. 
print encode("decodekey", "Username")
print encode("decodekey", "Password")

# Here we can get two string, we can use decode to confirm if they are right. In Start/Stop tool, they use decoded string to login adminWeb
# xdnNssfoyN_Y
# sdnUdfdfkkfdi9

print decode("decodekey","xdnNssfoyN_Y")
print decode("decodekey","sdnUdfdfkkfdi9")
# We get:
# Username
# Password

```

