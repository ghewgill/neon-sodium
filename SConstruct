import os
import shutil
import sys
import tarfile

env = Environment()
if sys.platform == "win32":
    env.Append(CXXFLAGS=["/EHsc", "/MDd", "/W4", "/WX"])
else:
    env.Append(CXXFLAGS=["-std=c++0x"])

libsodium = None

sodiumenv = Environment()
if "RELEASE" not in env or not env["RELEASE"]:
    if sys.platform == "win32":
        sodiumenv.Append(CFLAGS=[
            "/MDd",
            "/Zi",
            "/Od",
        ])

if GetOption("clean"):
    shutil.rmtree("libsodium-1.0.5", ignore_errors=True)
elif not os.path.exists("libsodium-1.0.5/configure"):
    tarfile.open("libsodium-1.0.5.tar.gz").extractall(".")
    if sys.platform == "win32":
        version = open("libsodium-1.0.5/src/libsodium/include/sodium/version.h.in").read()
        version = (version
            .replace("@VERSION@", "1.0.5")
            .replace("@SODIUM_LIBRARY_VERSION_MAJOR@", "7")
            .replace("@SODIUM_LIBRARY_VERSION_MINOR@", "6")
        )
        open("libsodium-1.0.5/src/libsodium/include/sodium/version.h", "w").write(version)

if sys.platform == "win32":
    sodiumenv.Append(CPPPATH=["libsodium-1.0.5/src/libsodium/include"])
    sodiumenv.Append(CPPPATH=["libsodium-1.0.5/src/libsodium/include/sodium"])
    sodiumenv.Append(CPPFLAGS=["-DSODIUM_STATIC"])
    sodiumenv.Append(CPPFLAGS=["-Dinline="])
    libsodium = sodiumenv.Library("libsodium-1.0.5/libsodium.lib", [
        "libsodium-1.0.5/src/libsodium/crypto_aead/aes256gcm/aesni/aead_aes256gcm_aesni.c",
        "libsodium-1.0.5/src/libsodium/crypto_aead/chacha20poly1305/sodium/aead_chacha20poly1305.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/crypto_auth.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha256/auth_hmacsha256_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha256/cp/hmac_hmacsha256.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha256/cp/verify_hmacsha256.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha512/auth_hmacsha512_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha512/cp/hmac_hmacsha512.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha512/cp/verify_hmacsha512.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha512256/auth_hmacsha512256_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha512256/cp/hmac_hmacsha512256.c",
        "libsodium-1.0.5/src/libsodium/crypto_auth/hmacsha512256/cp/verify_hmacsha512256.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/crypto_box.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/crypto_box_easy.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/crypto_box_seal.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/curve25519xsalsa20poly1305/box_curve25519xsalsa20poly1305_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/curve25519xsalsa20poly1305/ref/after_curve25519xsalsa20poly1305.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/curve25519xsalsa20poly1305/ref/before_curve25519xsalsa20poly1305.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/curve25519xsalsa20poly1305/ref/box_curve25519xsalsa20poly1305.c",
        "libsodium-1.0.5/src/libsodium/crypto_box/curve25519xsalsa20poly1305/ref/keypair_curve25519xsalsa20poly1305.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/hsalsa20/core_hsalsa20_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/hsalsa20/ref2/core_hsalsa20.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/salsa20/core_salsa20_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/salsa20/ref/core_salsa20.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/salsa2012/core_salsa2012_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/salsa2012/ref/core_salsa2012.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/salsa208/core_salsa208_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_core/salsa208/ref/core_salsa208.c",
        "libsodium-1.0.5/src/libsodium/crypto_generichash/blake2/generichash_blake2_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_generichash/blake2/ref/blake2b-ref.c",
        "libsodium-1.0.5/src/libsodium/crypto_generichash/blake2/ref/generichash_blake2b.c",
        "libsodium-1.0.5/src/libsodium/crypto_generichash/crypto_generichash.c",
        "libsodium-1.0.5/src/libsodium/crypto_hash/crypto_hash.c",
        "libsodium-1.0.5/src/libsodium/crypto_hash/sha256/cp/hash_sha256.c",
        "libsodium-1.0.5/src/libsodium/crypto_hash/sha256/hash_sha256_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_hash/sha512/cp/hash_sha512.c",
        "libsodium-1.0.5/src/libsodium/crypto_hash/sha512/hash_sha512_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_onetimeauth/crypto_onetimeauth.c",
        "libsodium-1.0.5/src/libsodium/crypto_onetimeauth/poly1305/donna/auth_poly1305_donna.c",
        "libsodium-1.0.5/src/libsodium/crypto_onetimeauth/poly1305/donna/verify_poly1305_donna.c",
        "libsodium-1.0.5/src/libsodium/crypto_onetimeauth/poly1305/onetimeauth_poly1305.c",
        "libsodium-1.0.5/src/libsodium/crypto_onetimeauth/poly1305/onetimeauth_poly1305_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_onetimeauth/poly1305/onetimeauth_poly1305_try.c",
        "libsodium-1.0.5/src/libsodium/crypto_pwhash/scryptsalsa208sha256/crypto_scrypt-common.c",
        "libsodium-1.0.5/src/libsodium/crypto_pwhash/scryptsalsa208sha256/nosse/pwhash_scryptsalsa208sha256_nosse.c",
        "libsodium-1.0.5/src/libsodium/crypto_pwhash/scryptsalsa208sha256/pbkdf2-sha256.c",
        "libsodium-1.0.5/src/libsodium/crypto_pwhash/scryptsalsa208sha256/pwhash_scryptsalsa208sha256.c",
        "libsodium-1.0.5/src/libsodium/crypto_pwhash/scryptsalsa208sha256/scrypt_platform.c",
        "libsodium-1.0.5/src/libsodium/crypto_pwhash/scryptsalsa208sha256/sse/pwhash_scryptsalsa208sha256_sse.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/crypto_scalarmult.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/donna_c64/base_curve25519_donna_c64.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/donna_c64/smult_curve25519_donna_c64.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/base_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_0_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_1_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_add_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_copy_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_cswap_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_frombytes_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_invert_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_mul121666_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_mul_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_sq_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_sub_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/fe_tobytes_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/ref10/scalarmult_curve25519_ref10.c",
        "libsodium-1.0.5/src/libsodium/crypto_scalarmult/curve25519/scalarmult_curve25519_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_secretbox/crypto_secretbox.c",
        "libsodium-1.0.5/src/libsodium/crypto_secretbox/crypto_secretbox_easy.c",
        "libsodium-1.0.5/src/libsodium/crypto_secretbox/xsalsa20poly1305/ref/box_xsalsa20poly1305.c",
        "libsodium-1.0.5/src/libsodium/crypto_secretbox/xsalsa20poly1305/secretbox_xsalsa20poly1305_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_shorthash/crypto_shorthash.c",
        "libsodium-1.0.5/src/libsodium/crypto_shorthash/siphash24/ref/shorthash_siphash24.c",
        "libsodium-1.0.5/src/libsodium/crypto_shorthash/siphash24/shorthash_siphash24_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/crypto_sign.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_0.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_1.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_add.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_cmov.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_copy.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_frombytes.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_invert.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_isnegative.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_isnonzero.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_mul.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_neg.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_pow22523.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_sq.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_sq2.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_sub.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/fe_tobytes.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_add.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_double_scalarmult.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_frombytes.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_madd.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_msub.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p1p1_to_p2.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p1p1_to_p3.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p2_0.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p2_dbl.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p3_0.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p3_dbl.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p3_tobytes.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p3_to_cached.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_p3_to_p2.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_precomp_0.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_scalarmult_base.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_sub.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/ge_tobytes.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/keypair.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/open.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/sc_muladd.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/sc_reduce.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/ref10/sign.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/ed25519/sign_ed25519_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/edwards25519sha512batch/ref/fe25519_edwards25519sha512batch.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/edwards25519sha512batch/ref/ge25519_edwards25519sha512batch.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/edwards25519sha512batch/ref/sc25519_edwards25519sha512batch.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/edwards25519sha512batch/ref/sign_edwards25519sha512batch.c",
        "libsodium-1.0.5/src/libsodium/crypto_sign/edwards25519sha512batch/sign_edwards25519sha512batch_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/portable/afternm_aes128ctr.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/portable/beforenm_aes128ctr.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/portable/common_aes128ctr.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/portable/consts_aes128ctr.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/portable/int128_aes128ctr.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/portable/stream_aes128ctr.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/portable/xor_afternm_aes128ctr.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/aes128ctr/stream_aes128ctr_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/chacha20/ref/stream_chacha20_ref.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/chacha20/stream_chacha20_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/crypto_stream.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa20/ref/stream_salsa20_ref.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa20/ref/xor_salsa20_ref.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa20/stream_salsa20_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa2012/ref/stream_salsa2012.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa2012/ref/xor_salsa2012.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa2012/stream_salsa2012_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa208/ref/stream_salsa208.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa208/ref/xor_salsa208.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/salsa208/stream_salsa208_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/xsalsa20/ref/stream_xsalsa20.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/xsalsa20/ref/xor_xsalsa20.c",
        "libsodium-1.0.5/src/libsodium/crypto_stream/xsalsa20/stream_xsalsa20_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_verify/16/ref/verify_16.c",
        "libsodium-1.0.5/src/libsodium/crypto_verify/16/verify_16_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_verify/32/ref/verify_32.c",
        "libsodium-1.0.5/src/libsodium/crypto_verify/32/verify_32_api.c",
        "libsodium-1.0.5/src/libsodium/crypto_verify/64/ref/verify_64.c",
        "libsodium-1.0.5/src/libsodium/crypto_verify/64/verify_64_api.c",
        "libsodium-1.0.5/src/libsodium/randombytes/nativeclient/randombytes_nativeclient.c",
        "libsodium-1.0.5/src/libsodium/randombytes/randombytes.c",
        "libsodium-1.0.5/src/libsodium/randombytes/salsa20/randombytes_salsa20_random.c",
        "libsodium-1.0.5/src/libsodium/randombytes/sysrandom/randombytes_sysrandom.c",
        "libsodium-1.0.5/src/libsodium/sodium/core.c",
        "libsodium-1.0.5/src/libsodium/sodium/runtime.c",
        "libsodium-1.0.5/src/libsodium/sodium/utils.c",
        "libsodium-1.0.5/src/libsodium/sodium/version.c",
    ])
    env.Append(CPPPATH=["libsodium-1.0.5/src/libsodium/include"])
    env.Append(CPPFLAGS=["-DSODIUM_STATIC"])
else:
    conf = Configure(env)
    if not conf.CheckLibWithHeader("sodium", "sodium.h", "C++"):
        libsodium = sodiumenv.Command("libsodium-1.0.5/src/libsodium/.libs/libsodium.a", "libsodium-1.0.5/configure", "cd libsodium-1.0.5 && ./configure --enable-pie=no && make")
        env.Append(CPPPATH=["libsodium-1.0.5/src/libsodium/include"])
    conf.Finish()

env.Append(CPPPATH="../../common")
env.Append(LIBS=[libsodium])
env.Depends("sodium.cpp", libsodium) # Ensure that header files are created.
env.SharedLibrary("neon_sodium", "sodium.cpp")
