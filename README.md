About
=====

SM3 Cryptographic Hash Algorithm is a chinese national cryptographic hash
algorithm standard published by the State Cryptography Administration Office 
of Security Commercial Code Administration (OSCCA) of China in December 2010.
A draft of this algorithm can be found at

[http://tools.ietf.org/html/draft-shen-sm3-hash-00](http://tools.ietf.org/html/draft-shen-sm3-hash-00 "RFC Draft")


The SM3 take input messages as 512 bits blocks and generates
256 bits digest values, same as SHA-256.

This project provides an open source C implementation of SM3 hash
algorithm. The project includes a library with init, update, final style of
interfaces and an command line tool.

Install
=======

	./configure
	make
	sudo make install


Try the command line tool

	echo -n abc | sm3
	66c7f0f462eeedd9d1f2d46bdc10e4e24167c4875cf2f7a2297da02b8f4ba8e0

If libsm3.so can not be found on Linux, run

	sudo ldconfig -v

Usage
=====

The libsm3 library provides the following C API:

	void sm3_init(sm3_ctx_t *ctx);
	void sm3_update(sm3_ctx_t *ctx, const unsigned char* data, size_t data_len);
	void sm3_final(sm3_ctx_t *ctx, unsigned char digest[SM3_DIGEST_LENGTH]);
	void sm3_compress(uint32_t digest[8], const unsigned char block[SM3_BLOCK_SIZE]);
	void sm3(const unsigned char *data, size_t datalen, unsigned char digest[SM3_DIGEST_LENGTH]);

	void hmac_sm3_init(hmac_sm3_ctx_t *ctx, const unsigned char *key, size_t key_len);
	void hmac_sm3_update(hmac_sm3_ctx_t *ctx, const unsigned char *data, size_t data_len);
	void hmac_sm3_final(hmac_sm3_ctx_t *ctx, unsigned char mac[HMAC_SM3_MAC_SIZE]);
	void hmac_sm3(const unsigned char *data, size_t data_len,
		const unsigned char *key, size_t key_len, unsigned char mac[HMAC_SM3_MAC_SIZE]);

Example on using C API to digest a message:

	unsigend char buffer[SM3_DIGEST_LENGTH];
	sm3("hello", strlen("hello"), buffer);

Example on using C API to digest a stream:

	unsigned char dgst[SM3_DIGEST_LENGTH];
	sm3_ctx_t ctx;
	sm3_init(&ctx);
	sm3_update(&ctx, "hello", strlen("hello"));
	sm3_update(&ctx, "world", strlen("world"));
	sm3_final(&ctx, dgst);

Example on using C API to generate a HMAC tag:

	unsigned char mac[HMAC_SM3_MAC_SIZE];
	hmac_sm3_ctx_t ctx;
	unsigned char key[16];
	hmac_sm3_init(&ctx, key, sizeof(key));
	hmac_sm3_update(&ctx, "hello", strlen("hello"));
	hmac_sm3_update(&ctx, "world", strlen("world"));
	hmac_sm3_final(&ctx, mac);

Benchmark
=========

To be add ...
