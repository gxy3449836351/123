#include <stdio.h>

#include <stdlib.h>

#include <string.h>



typedef struct {

    char character;

    char* code;

} HuffmanNode;



void printHuffmanCodes(HuffmanNode* huffmanTree, int numNodes) {

    printf("\n%d个字符的哈夫曼编码如下：\n", numNodes);

    for (int i = 0; i < numNodes; i++) {

        printf("<%c>编码：%s\n", huffmanTree[i].character, huffmanTree[i].code);

    }

}



void traverseHuffmanTree(HuffmanNode* huffmanTree, int index, char* code, int depth) {

    if (index < 0) {

        return;

    }

    

    if (index < 256) {

        huffmanTree[index].code = malloc((depth + 1) * sizeof(char));

        strcpy(huffmanTree[index].code, code);

        huffmanTree[index].code[depth] = '\0';

    }

    

    if (index * 2 + 1 < 512) {

        char* leftCode = malloc((depth + 1) * sizeof(char));

        strcpy(leftCode, code);

        leftCode[depth] = '0';

        traverseHuffmanTree(huffmanTree, index * 2 + 1, leftCode, depth + 1);

        free(leftCode);

    }

    

    if (index * 2 + 2 < 512) {

        char* rightCode = malloc((depth + 1) * sizeof(char));

        strcpy(rightCode, code);

        rightCode[depth] = '1';

        traverseHuffmanTree(huffmanTree, index * 2 + 2, rightCode, depth + 1);

        free(rightCode);

    }

}



HuffmanNode* generateHuffmanTree() {

    int numNodes = 6;

    HuffmanNode* huffmanTree = malloc(512 * sizeof(HuffmanNode));

    

    for (int i = 0; i < numNodes; i++) {

        huffmanTree[i].character = i;

        huffmanTree[i].code = NULL;

    }

    

    traverseHuffmanTree(huffmanTree, 0, "", 0);

    

    return huffmanTree;

}



char* encode(char* str) {

    int len = strlen(str);

    char* encoded = malloc((2 * len + 1) * sizeof(char));

    

    HuffmanNode* huffmanTree = generateHuffmanTree();

    

    for (int i = 0; i < len; i++) {

        char* code = huffmanTree[(int)str[i]].code;

        encoded[2 * i] = code[0];

        encoded[2 * i + 1] = ' ';

    }

    encoded[2 * len] = '\0';

    

    printHuffmanCodes(huffmanTre
