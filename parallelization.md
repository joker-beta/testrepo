{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'\\n输入: \\n        Q1 = ((w11, b11), (w12, b12),..,(w1n, b1n))\\n        Q2 = ((w21, b21), (w22, b22),..,(w2n, b2n))\\n输出:\\n        Q = ((w1, b1), (w2, b2),...,(wn, bn))\\n\\n其中:\\n        w1 = [w11] , b1 = [b11] ,  wi = [w1i  0 ] , bi = [b1i]\\n             [w12]        [b12]         [ 0  w2i]        [b2i]\\n                                       ( i = 2,3,...,n)\\n---------------------------------------------\\n'"
      ]
     },
     "execution_count": 1,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import numpy as np\n",
    "import Ipynb_importer\n",
    "from scipy.linalg import block_diag   # 分块对角矩阵\n",
    "\n",
    "\"\"\"\n",
    "            输入: \n",
    "                    Q1 = ((w11, b11), (w12, b12),..,(w1n, b1n))\n",
    "                    Q2 = ((w21, b21), (w22, b22),..,(w2n, b2n))\n",
    "            输出:\n",
    "                    Q = ((w1, b1), (w2, b2),...,(wn, bn))\n",
    "\n",
    "            其中:\n",
    "                    w1 = [w11] , b1 = [b11] ,  wi = [w1i  0 ] , bi = [b1i]\n",
    "                         [w12]        [b12]         [ 0  w2i]        [b2i]\n",
    "                                                   ( i = 2,3,...,n)\n",
    "---------------------------------------------------------------------------\n",
    "\"\"\""
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [],
   "source": [
    "# 输入:\n",
    "    # Q1, Q2: 两个待并联的子网络\n",
    "# 输出:\n",
    "    # 并联之后的总网络\n",
    "def parallelization(Q1, Q2):\n",
    "    \"\"\"网络并联\"\"\"\n",
    "    \n",
    "    if (len(Q1) != len(Q2)) or (len(Q1) == 0) or (len(Q2) == 0):\n",
    "        return None\n",
    "    else:\n",
    "        total_Q = []\n",
    "        \n",
    "        # 第一组元素\n",
    "        w1 = np.vstack((Q1[0][0], Q2[0][0]))\n",
    "        b1 = np.vstack((Q1[0][1], Q2[0][1]))\n",
    "        Q = (w1, b1)\n",
    "        \n",
    "        total_Q.append(Q)\n",
    "        # 后面的各组元素\n",
    "        for i in range(1, len(Q1)):\n",
    "                \n",
    "            wi = block_diag(Q1[i][0], Q2[i][0])\n",
    "            bi = np.vstack((Q1[i][1], Q2[i][1]))\n",
    "            Q = (wi, bi)\n",
    "            \n",
    "            total_Q.append(Q)\n",
    "\n",
    "    return total_Q\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
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
   "version": "3.6.9"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}
