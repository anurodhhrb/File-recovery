#include <stdio.h>
#include <stdlib.h>
int main (int argc, char * argv[])
{
    // checking for the correct amount of arguments
    if (argc != 2)
    {
        fprintf(stderr, "Usage: recover card.raw");
        return 1;
    }
  // initializing the counter to zero
  int counter = 0;
  //storing the address of the argument vector
  char *card = argv[1];
  unsigned char buffer[512];
  int checker = 0;
  //opening the card and storing the address of the card in file pointer.
  FILE *inptr = fopen(card, "r");
  //sanity check
  if (inptr == NULL)
    {
        fprintf(stderr, "Could not open %s.\n", card);
        return 2;
    }
//initializing file pointer to null

FILE *img = NULL;
//reading one block of 512 bytes each from the input pointer and storing it in a buffer
fread (buffer, 512, 1, inptr);

while (fread (buffer, 512, 1, inptr) > 0)
 {

     if (buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff && (buffer[3] & 0xf0) == 0xe0)
     {

         if (checker == 1)
         {
             fclose(img);
         }
         if (checker == 0)
         {
             //fwrite (&buffer, sizeof(buffer), 1, img);
             checker = 1;
             // = 1;
         }
             char image[8];
             sprintf(image, "%03d.jpg", counter);
             img = fopen(image, "a");
             counter += 1;
             if (checker == 1)
             {
             fwrite (&buffer, sizeof(buffer), 1, img);
             }

     }
     else
     {  if (img != NULL)
         fwrite(&buffer, sizeof(buffer), 1, img);
     }
 }

fclose(inptr);
fclose (img);
return 0;
}
