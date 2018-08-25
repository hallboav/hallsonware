# Hallsonware

Escrito em JScript.

Use SOMENTE em ambiente controlado e para fins de aprendizado.

## Como funciona

Para um arquivo alvo (Ex.: `message.txt`) é gerada uma chave aleatória de 256 bytes (`message.txt.key`) e esta é
usada para cifrá-lo, dando origem ao arquivo alvo cifrado (`message.txt.enc`). Desta forma, temos uma chave 
descriptográfica para cada arquivo.

```shell
hall@localhost:/tmp/hallsonware $ hexdump -C message.txt
00000000  54 68 65 72 65 20 69 73  20 6e 6f 20 73 70 6f 6f  |There is no spoo|
00000010  6e 2e 0a                                          |n..|
00000013
```

```shell
hall@localhost:/tmp/hallsonware $ hexdump -C message.txt.key
00000000  32 d9 be af f9 d2 6a 2f  cf 6f f5 26 4b 5d 90 57  |2.....j/.o.&K].W|
00000010  fd 52 2a cf 94 e7 15 7b  d1 c1 71 6c 69 18 96 1b  |.R*....{..qli...|
00000020  b4 9f b8 4b f9 fa 81 bf  87 6e de a8 78 a4 85 10  |...K.....n..x...|
00000030  df c2 36 c2 bf 4b 8d 00  c5 bb 41 50 f9 0f c1 31  |..6..K....AP...1|
00000040  a3 d4 0e 3e 3e e7 be 70  8e e3 71 73 86 6e 0d 25  |...>>..p..qs.n.%|
00000050  d0 7f 25 fc ae 45 fa e0  9b 02 cb 99 32 90 05 78  |..%..E......2..x|
00000060  70 bb 18 b8 f8 ce 7c 81  70 71 1b 7d 3d dd 79 30  |p.....|.pq.}=.y0|
00000070  c5 7b 2e 4e 12 ef c3 eb  03 82 11 a0 36 68 34 cc  |.{.N........6h4.|
00000080  18 d6 8d 88 e9 64 bf c2  a7 fd d2 12 18 43 eb 89  |.....d.......C..|
00000090  26 cd 9c 03 74 2b f6 e9  9d 6d ef 37 a1 8d 3a dd  |&...t+...m.7..:.|
000000a0  06 43 0b f5 62 57 b9 22  1f f1 35 87 6b 7f f9 cf  |.C..bW."..5.k...|
000000b0  ef 7f fe df 02 eb 90 6d  56 b1 a8 57 fb 92 71 87  |.......mV..W..q.|
000000c0  d2 4b fd c8 63 fd 22 ae  5f af cd bd 73 76 7a 31  |.K..c."._...svz1|
000000d0  a9 ec 6a 94 54 59 8e 66  cc f7 a4 91 25 ad 55 13  |..j.TY.f....%.U.|
000000e0  e4 57 64 84 4b 0e bc f7  ee 9d b3 31 70 62 4a d6  |.Wd.K......1pbJ.|
000000f0  df 2a 6c cd 28 85 54 3a  f3 2a be 68 6b dd 7b e9  |.*l.(.T:.*.hk.{.|
00000100
```

```shell
hall@localhost:/tmp/hallsonware $ hexdump -C message.txt.enc
00000000  53 61 6c 74 65 64 5f 5f  e3 7c af a8 41 4f 7a 31  |Salted__.|..AOz1|
00000010  15 72 2a 92 d5 9e d6 84  09 12 8c 1e 7f 44 be 5d  |.r*..........D.]|
00000020  c6 3b 4e 72 a3 ad d0 ee  f6 72 3b b6 9a 80 74 1a  |.;Nr.....r;...t.|
00000030
```

A chave descriptográfica (`message.txt.key`) usada para cifrar o arquivo alvo é cifrada usando a chave pública, dando
origem à chave cifrada (`message.txt.key.enc`). Após o passo anterior, a chave (`message.txt.key`) e o arquivo 
(`message.txt`) original são deletados.

```shell
hall@localhost:/tmp/hallsonware $ hexdump -C message.txt.key.enc 
00000000  05 bf 57 71 bd 41 45 d8  a7 5b 5f 05 c9 c0 b1 98  |..Wq.AE..[_.....|
00000010  18 7b 8e 21 34 63 cf a0  80 e9 2b 46 ab fe 5c 78  |.{.!4c....+F..\x|
00000020  e8 0d b8 4d aa c4 b3 fe  e3 88 e9 cc 20 3d 3e 8b  |...M........ =>.|
00000030  da b9 51 09 ae df cc 22  ba 7a 35 1e 98 36 cf dc  |..Q....".z5..6..|
00000040  31 65 8c 9b f6 fa 70 0a  12 86 86 3c 5b 11 ab 4b  |1e....p....<[..K|
00000050  94 02 a0 26 8e 68 6c e1  84 5e 19 fc 44 cb 42 84  |...&.hl..^..D.B.|
00000060  da ea b8 8c fa 12 75 1a  67 44 4a f0 b9 22 3f ca  |......u.gDJ.."?.|
00000070  e4 48 32 3d 93 79 da 3b  33 2f 5e ee 37 77 29 f6  |.H2=.y.;3/^.7w).|
00000080  88 bb 39 0b bf c1 64 be  e7 75 2a 7c 03 fa dd 6c  |..9...d..u*|...l|
00000090  56 51 07 7b e1 11 52 67  c8 fc 84 74 fe 7c 3a a9  |VQ.{..Rg...t.|:.|
000000a0  1e 12 ef e4 f5 2e 55 cf  a3 d2 d3 4b f3 bc 4d 87  |......U....K..M.|
000000b0  30 05 42 c3 ca 58 c3 2b  aa 5d b5 d6 90 f1 b0 fe  |0.B..X.+.]......|
000000c0  05 97 42 82 de 04 b7 ab  f8 40 44 86 39 14 78 7e  |..B......@D.9.x~|
000000d0  93 90 30 93 cd 34 da 04  ab 76 c5 57 b9 65 21 36  |..0..4...v.W.e!6|
000000e0  37 bf bc 9b b5 ba de 74  61 b7 55 17 2c 4e 22 7b  |7......ta.U.,N"{|
000000f0  e0 f9 02 38 86 4c 92 a3  3f d1 44 02 f4 ba 6d 01  |...8.L..?.D...m.|
00000100  e6 d0 00 38 60 70 55 f6  d2 b3 f9 a4 6e 47 5f 25  |...8`pU.....nG_%|
00000110  40 38 2f 94 f8 ab 7a 45  d0 bd ba 42 0b c0 39 73  |@8/...zE...B..9s|
00000120  f4 f6 29 de 3a 5f db e2  7a 68 29 d8 7f 18 2b 6f  |..).:_..zh)...+o|
00000130  9e d1 e8 1c 14 cf 98 d7  99 fd 1f e3 9d 4b 3e bc  |.............K>.|
00000140  72 1d 49 a6 c6 6a b7 1c  df 0f 9c 26 1d e6 8f c9  |r.I..j.....&....|
00000150  4b 9a 50 39 de 83 ef 9b  26 33 56 72 36 f5 08 cf  |K.P9....&3Vr6...|
00000160  d8 74 62 e3 16 82 3a f8  fe b7 61 5b 55 cb 07 73  |.tb...:...a[U..s|
00000170  e2 61 8a b4 a1 68 66 52  61 91 84 60 cd ef e3 2b  |.a...hfRa..`...+|
00000180  a5 b2 7f 82 58 78 9a e8  6c 16 b9 ec 5e 48 45 fe  |....Xx..l...^HE.|
00000190  61 d8 fc f5 6c 62 10 5e  94 8a af 68 39 ae f7 e9  |a...lb.^...h9...|
000001a0  84 3a 62 fa 7d 7d 08 e4  86 56 77 ef 13 b0 8b 1e  |.:b.}}...Vw.....|
000001b0  ff 44 73 96 e4 03 db 26  4d 0c a3 70 59 55 1d b3  |.Ds....&M..pYU..|
000001c0  e8 4d fc b7 47 e6 74 0b  9c 56 10 89 17 a0 84 4d  |.M..G.t..V.....M|
000001d0  fc 6e bf 54 f6 95 ae 0b  86 50 00 7c 7e 34 68 69  |.n.T.....P.|~4hi|
000001e0  ac a7 c7 bb ea 95 bf 6c  62 9f b9 40 40 fb 3e bc  |.......lb..@@.>.|
000001f0  69 31 5d e9 05 06 2f 38  27 a2 a8 2a 12 c8 a7 b5  |i1].../8'..*....|
00000200
```

Temos então, apenas informações cifradas dos arquivos, que são juntadas em um único arquivo (`message.txt.enc`) da seguinte forma:

```shell
hall@localhost:/tmp/hallsonware $ hexdump -C message.txt.enc
00000000  05 bf 57 71 bd 41 45 d8  a7 5b 5f 05 c9 c0 b1 98  |..Wq.AE..[_.....|
00000010  18 7b 8e 21 34 63 cf a0  80 e9 2b 46 ab fe 5c 78  |.{.!4c....+F..\x|
00000020  e8 0d b8 4d aa c4 b3 fe  e3 88 e9 cc 20 3d 3e 8b  |...M........ =>.|
00000030  da b9 51 09 ae df cc 22  ba 7a 35 1e 98 36 cf dc  |..Q....".z5..6..|
00000040  31 65 8c 9b f6 fa 70 0a  12 86 86 3c 5b 11 ab 4b  |1e....p....<[..K|
00000050  94 02 a0 26 8e 68 6c e1  84 5e 19 fc 44 cb 42 84  |...&.hl..^..D.B.|
00000060  da ea b8 8c fa 12 75 1a  67 44 4a f0 b9 22 3f ca  |......u.gDJ.."?.|
00000070  e4 48 32 3d 93 79 da 3b  33 2f 5e ee 37 77 29 f6  |.H2=.y.;3/^.7w).|
00000080  88 bb 39 0b bf c1 64 be  e7 75 2a 7c 03 fa dd 6c  |..9...d..u*|...l|
00000090  56 51 07 7b e1 11 52 67  c8 fc 84 74 fe 7c 3a a9  |VQ.{..Rg...t.|:.|
000000a0  1e 12 ef e4 f5 2e 55 cf  a3 d2 d3 4b f3 bc 4d 87  |......U....K..M.|
000000b0  30 05 42 c3 ca 58 c3 2b  aa 5d b5 d6 90 f1 b0 fe  |0.B..X.+.]......|
000000c0  05 97 42 82 de 04 b7 ab  f8 40 44 86 39 14 78 7e  |..B......@D.9.x~|
000000d0  93 90 30 93 cd 34 da 04  ab 76 c5 57 b9 65 21 36  |..0..4...v.W.e!6|
000000e0  37 bf bc 9b b5 ba de 74  61 b7 55 17 2c 4e 22 7b  |7......ta.U.,N"{|
000000f0  e0 f9 02 38 86 4c 92 a3  3f d1 44 02 f4 ba 6d 01  |...8.L..?.D...m.|
00000100  e6 d0 00 38 60 70 55 f6  d2 b3 f9 a4 6e 47 5f 25  |...8`pU.....nG_%|
00000110  40 38 2f 94 f8 ab 7a 45  d0 bd ba 42 0b c0 39 73  |@8/...zE...B..9s|
00000120  f4 f6 29 de 3a 5f db e2  7a 68 29 d8 7f 18 2b 6f  |..).:_..zh)...+o|
00000130  9e d1 e8 1c 14 cf 98 d7  99 fd 1f e3 9d 4b 3e bc  |.............K>.|
00000140  72 1d 49 a6 c6 6a b7 1c  df 0f 9c 26 1d e6 8f c9  |r.I..j.....&....|
00000150  4b 9a 50 39 de 83 ef 9b  26 33 56 72 36 f5 08 cf  |K.P9....&3Vr6...|
00000160  d8 74 62 e3 16 82 3a f8  fe b7 61 5b 55 cb 07 73  |.tb...:...a[U..s|
00000170  e2 61 8a b4 a1 68 66 52  61 91 84 60 cd ef e3 2b  |.a...hfRa..`...+|
00000180  a5 b2 7f 82 58 78 9a e8  6c 16 b9 ec 5e 48 45 fe  |....Xx..l...^HE.|
00000190  61 d8 fc f5 6c 62 10 5e  94 8a af 68 39 ae f7 e9  |a...lb.^...h9...|
000001a0  84 3a 62 fa 7d 7d 08 e4  86 56 77 ef 13 b0 8b 1e  |.:b.}}...Vw.....|
000001b0  ff 44 73 96 e4 03 db 26  4d 0c a3 70 59 55 1d b3  |.Ds....&M..pYU..|
000001c0  e8 4d fc b7 47 e6 74 0b  9c 56 10 89 17 a0 84 4d  |.M..G.t..V.....M|
000001d0  fc 6e bf 54 f6 95 ae 0b  86 50 00 7c 7e 34 68 69  |.n.T.....P.|~4hi|
000001e0  ac a7 c7 bb ea 95 bf 6c  62 9f b9 40 40 fb 3e bc  |.......lb..@@.>.|
000001f0  69 31 5d e9 05 06 2f 38  27 a2 a8 2a 12 c8 a7 b5  |i1].../8'..*....|
00000200  53 61 6c 74 65 64 5f 5f  e3 7c af a8 41 4f 7a 31  |Salted__.|..AOz1|
00000210  15 72 2a 92 d5 9e d6 84  09 12 8c 1e 7f 44 be 5d  |.r*..........D.]|
00000220  c6 3b 4e 72 a3 ad d0 ee  f6 72 3b b6 9a 80 74 1a  |.;Nr.....r;...t.|
00000230
```

### Decifrando

Para decifrar:

1. Separar o arquivo cifrado nos dois que o compoem: `message.txt.key.enc` (primeiros 512 bytes) e `message.txt.enc`.
2. Usar a chave privada `private.pem` para decifrar a chave do arquivo original `message.txt.key.enc`, dando existência
ao `message.txt.key`.
3. Usar a chave `message.txt.key` para decifrar `message.txt.enc`, obtendo assim o `message.txt`.

## Como usar

Construção:

1. Configure `targetFolders` e `targetExtensions` no final do arquivo `hallsonware.js`.
3. Diminua o tamanho do arquivo final com `npm i && node_modules/minify/bin/minify.js hallsonware.js > Document.docx.js` (opcional).
4. Numa máquina com SO Windows dê um click duplo no `Document.docx.js`.

## Todo

- [ ] Adicionar método de Gutmann [https://en.wikipedia.org/wiki/Gutmann_method](https://en.wikipedia.org/wiki/Gutmann_method)
