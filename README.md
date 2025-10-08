# EX 3 : Circle Drawing Algorithm

**AIM :**

To  implement the Bresenham’s  algorithm for circle using a c coding.


**ALGORITHM :**

Step 1 : Start.
    
Step 2 : Initialize the graphics header files and functions.
   
Step 3 : Declare the required variables and functions.
 
Step 4 : Get the co-ordinates and radius of the circle.

Step 5 : Draw the circle using the algorithm.

Step  6 : Display the output.
  
Step 7 : stop.

**Program :**
```
#include <graphics.h>
#include <stdio.h>
#include <conio.h>
#include <math.h>

void main()
{
    int gd = DETECT, gm, i, j, k, ch;
    float tx, ty, x, y, ang, n, temp;
    float a[5][3], si, co, b[5][3], c[5][3];

    initgraph(&gd, &gm, "c:\\turboc3\\bgi");
    n = 4;

    a[0][0] = 0;   a[0][1] = 0;
    a[1][0] = 100; a[1][1] = 0;
    a[2][0] = 100; a[2][1] = 100;
    a[3][0] = 0;   a[3][1] = 100;
    a[4][0] = 0;   a[4][1] = 0;

    while (1)
    {
        cleardevice();
        gotoxy(1, 8);

        printf("\n\t******** Program to perform 2-D Transformations ********");
        printf("\n\t\t\t 1. Accept the polygon");
        printf("\n\t\t\t 2. Perform translation");
        printf("\n\t\t\t 3. Perform scaling");
        printf("\n\t\t\t 4. Perform rotation");
        printf("\n\t\t\t 5. Perform reflection");
        printf("\n\t\t\t 6. Perform shearing");
        printf("\n\t\t\t 7. Exit");

        printf("\n\t\t\t Enter your choice::");
        scanf("%d", &ch);

        switch (ch)
        {
            case 1:
                cleardevice();
                gotoxy(1, 1);
                printf("\n\tEnter no of points.:");
                scanf("%f", &n);

                for (i = 0; i < n; i++)
                {
                    printf("\n\t Enter x,y co-ordinates for %d::", i + 1);
                    scanf("%f %f", &a[i][0], &a[i][1]);
                }
                a[i][0] = a[0][0];
                a[i][1] = a[0][1];

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 2:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("Enter translation vectors tx and ty\n\t");
                scanf("%f %f", &x, &y);

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0] + x, 240 - (a[i][1] + y), 320 + a[i + 1][0] + x, 240 - (a[i + 1][1] + y));

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 3:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("Enter scaling vectors tx and ty\n\t");
                scanf("%f %f", &x, &y);

                if (x == 0) x = 1;
                if (y == 0) y = 1;

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + (a[i][0] * x), 240 - (a[i][1] * y), 320 + (a[i + 1][0] * x), 240 - (a[i + 1][1] * y));

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 4:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("Enter the angle of rotation\n\t");
                scanf("%f", &ang);

                ang = ang * 0.01745;

                gotoxy(1, 3);
                printf("Enter point of rotation\n\t");
                scanf("%f %f", &x, &y);

                gotoxy(1, 5);
                printf("1.clockwise  2.anticlockwise\n\t");
                scanf("%d", &k);

                si = sin(ang);
                co = cos(ang);

                for (i = 0; i < n + 1; i++)
                {
                    c[i][0] = a[i][0];
                    c[i][1] = a[i][1];
                    c[i][2] = 1;
                }

                b[0][0] = co;    b[0][1] = si;    b[0][2] = 0;
                b[1][0] = -si;   b[1][1] = co;    b[1][2] = 0;
                b[2][0] = -x * co + (y * si) + x;
                b[2][1] = -x * si - (y * co) + y;
                b[2][2] = 1;

                if (k == 1)
                {
                    b[0][1] = -si;
                    b[1][0] = si;
                    b[2][0] = -x * co - (y * si) + x;
                    b[2][1] = -x * si + (y * co) + y;
                }

                for (i = 0; i < n + 1; i++)
                {
                    for (j = 0; j < 3; j++)
                    {
                        a[i][j] = 0;
                        for (k = 0; k < 3; k++)
                            a[i][j] = a[i][j] + c[i][k] * b[k][j];
                    }
                }

                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);
                getch();
                break;

            case 5:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("\n1.Reflection about Y-axis");
                printf("\n2.Reflection about X-axis");
                printf("\n3.Reflection about origin");
                printf("\n4.Reflection about line y=x");
                printf("\n5.Reflection about line y=-x");
                printf("\nEnter your choice:");
                scanf("%d", &ch);

                switch (ch)
                {
                    case 1:
                        for (i = 0; i < n + 1; i++)
                            a[i][0] = a[i][0] * -1;

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 2:
                        for (i = 0; i < n + 1; i++)
                            a[i][1] = a[i][1] * -1;

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 3:
                        for (i = 0; i < n + 1; i++)
                        {
                            a[i][1] = a[i][1] * -1;
                            a[i][0] = a[i][0] * -1;
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 4:
                        for (i = 0; i < n + 1; i++)
                        {
                            temp = a[i][0];
                            a[i][0] = a[i][1];
                            a[i][1] = temp;
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        line(0, 479, 639, 0);
                        getch();
                        break;

                    case 5:
                        for (i = 0; i < n + 1; i++)
                        {
                            temp = a[i][0];
                            a[i][0] = a[i][1];
                            a[i][1] = temp;
                        }

                        for (i = 0; i < n + 1; i++)
                        {
                            a[i][1] = a[i][1] * -1;
                            a[i][0] = a[i][0] * -1;
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        line(0, 0, 639, 479);
                        getch();
                        break;

                    default:
                        break;
                }
                break;

            case 6:
                cleardevice();
                for (i = 0; i < n; i++)
                    line(320 + a[i][0], 240 - a[i][1], 320 + a[i + 1][0], 240 - a[i + 1][1]);

                line(0, 240, 639, 240);
                line(320, 0, 320, 479);

                gotoxy(1, 1);
                printf("\n1.X shear with y reference line");
                printf("\n2.Y shear with x reference line");
                printf("\nEnter your choice:");
                scanf("%d", &ch);

                switch (ch)
                {
                    case 1:
                        printf("\nEnter the x-shear parameter value:");
                        scanf("%f", &temp);
                        printf("\nEnter the yref line");
                        scanf("%f", &ty);

                        b[0][0] = 1;       b[0][1] = 0;       b[0][2] = 0;
                        b[1][0] = temp;    b[1][1] = 1;       b[1][2] = 0;
                        b[2][0] = -temp * ty;
                        b[2][1] = 0;       b[2][2] = 1;

                        for (i = 0; i < n + 1; i++) a[i][2] = 1;

                        for (i = 0; i < n + 1; i++)
                        {
                            for (j = 0; j < 3; j++)
                            {
                                c[i][j] = 0;
                                for (k = 0; k < 3; k++)
                                    c[i][j] = c[i][j] + a[i][k] * b[k][j];
                            }
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + c[i][0], 240 - c[i][1], 320 + c[i + 1][0], 240 - c[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    case 2:
                        printf("\nEnter the y-shear parameter value:");
                        scanf("%f", &temp);
                        printf("\nEnter the xref line");
                        scanf("%f", &tx);

                        b[0][0] = 1;       b[0][1] = temp;    b[0][2] = 0;
                        b[1][0] = 0;       b[1][1] = 1;       b[1][2] = 0;
                        b[2][0] = 0;       b[2][1] = -temp * tx; b[2][2] = 0;

                        for (i = 0; i < n + 1; i++) a[i][2] = 1;

                        for (i = 0; i < n + 1; i++)
                        {
                            for (j = 0; j < 3; j++)
                            {
                                c[i][j] = 0;
                                for (k = 0; k < 3; k++)
                                    c[i][j] = c[i][j] + a[i][k] * b[k][j];
                            }
                        }

                        cleardevice();
                        for (i = 0; i < n; i++)
                            line(320 + c[i][0], 240 - c[i][1], 320 + c[i + 1][0], 240 - c[i + 1][1]);

                        line(0, 240, 639, 240);
                        line(320, 0, 320, 479);
                        getch();
                        break;

                    default:
                        break;
                }
                break;

            case 7:
                exit(1);
                closegraph();
                restorecrtmode();
                break;

            default:
                break;
        }
    }
}

```



**Output :**
# polygon dimension
<img width="632" height="442" alt="494278763-96fa4f2c-18a0-4870-9fe2-9b6a78f15446" src="https://github.com/user-attachments/assets/8e25d9c3-84d0-435b-9964-03372288c874" />
<img width="601" height="412" alt="494278844-3e95c773-83f0-405a-9731-537c39d90a1b" src="https://github.com/user-attachments/assets/89313f14-51d1-445f-9af5-5f8983cb83fd" />





<img width="627" height="468" alt="494278905-24c8fad4-8231-433d-b338-5d54db23e2ce" src="https://github.com/user-attachments/assets/0fb1252c-4b0e-4c7e-8db4-3dc65b3e10c3" />

# Translation


<img width="632" height="442" alt="494280596-dbca2cf2-1d37-4ea3-881c-6b3e7e60ce9b" src="https://github.com/user-attachments/assets/99c7ed1b-742a-452e-a65b-5f3aa96eae58" />




<img width="635" height="482" alt="494280686-342440a0-5165-4bbd-b9bf-3ed634813504" src="https://github.com/user-attachments/assets/bd42ad4f-5c4b-4ab9-ba74-725e70c1448d" />


<img width="631" height="458" alt="494280779-560b4977-3c8d-4a3c-9ec4-9c61b4af8b69" src="https://github.com/user-attachments/assets/d7add3bf-d8e9-42a5-8469-cd8eab52bfb9" />



# scaling





<img width="635" height="473" alt="494281273-311b426b-18fa-4f24-a37d-b8f0791bd509" src="https://github.com/user-attachments/assets/e3368dbb-7911-49ff-8f86-0e74d502ef26" />



<img width="638" height="473" alt="494281360-be5d5c44-f4c3-4d2a-85dd-6763618ff09d" src="https://github.com/user-attachments/assets/bf6d576f-e99a-41d3-9caa-8d73da92b7ec" />





<img width="633" height="477" alt="494281405-74f34a48-6f02-417a-a1d3-c36b9cab15d6" src="https://github.com/user-attachments/assets/64b69089-b00e-4f79-95be-ac2d382c1c7b" />



# rotation

<img width="635" height="468" alt="494283037-6a72f345-13e6-4de7-a411-0d6903926b54" src="https://github.com/user-attachments/assets/683f79f3-1f8f-44cf-bbae-92933fa0fe25" />

# clockwise





<img width="636" height="482" alt="494285187-e28d225d-c1eb-498e-bb44-70d3e9b74427" src="https://github.com/user-attachments/assets/92f12eee-8dc7-43b6-9887-b6a1d50844f8" />





<img width="637" height="482" alt="494285237-e85b5adb-0cb9-4142-877e-09eed229927d" src="https://github.com/user-attachments/assets/6ffdf3f1-c678-4d42-983d-1fc3f59d9594" />

# anti clock wise




<img width="637" height="478" alt="494285360-07c7292b-941f-4fbe-b450-2d14118766b0" src="https://github.com/user-attachments/assets/af9fdf8d-0e8e-4f02-bfb1-e164db4e7000" />



<img width="637" height="471" alt="494285397-d738a6b2-cce4-413c-a0c8-7bf2a55fd3c3" src="https://github.com/user-attachments/assets/c25c8f83-062c-4add-a845-cfebad18e68d" />



# reflection

<img width="635" height="472" alt="494295625-3caa1578-e197-4aed-a0c5-32e86ed08cca" src="https://github.com/user-attachments/assets/59b2fbaa-e746-4ec7-a657-a0680acb6137" />

# reflection about y axis

<img width="638" height="476" alt="494295796-833708b4-ac20-4e6c-ad8d-bf29bc3af4e0" src="https://github.com/user-attachments/assets/adc795b1-2ae3-4a9d-9b77-da1749d00362" />





<img width="635" height="478" alt="494295841-e98d0a90-4cb7-40c9-8478-4c2e5a815bb7" src="https://github.com/user-attachments/assets/18c97bb6-4b42-47f7-9b17-9584eb2ffdd9" />

# reflection about x axis



<img width="641" height="482" alt="494322237-6ec67745-4abc-43c1-a7ae-267757876a8f" src="https://github.com/user-attachments/assets/8c425463-ead8-421f-8fc4-42a750187633" />




<img width="642" height="478" alt="494322274-94cf068f-9234-49f6-8417-08a463fe7682" src="https://github.com/user-attachments/assets/a29cdd5d-5926-4c5b-824f-72bd2a4cf56c" />


# reflection about orgin





<img width="638" height="466" alt="494296460-91ceed57-2d3c-49d5-a808-b039321558a7" src="https://github.com/user-attachments/assets/ca3f9a3c-37ae-4149-82a1-95a820e0afdf" />


<img width="637" height="477" alt="494296501-86bbbbbe-9990-45b6-ba52-f587ea48df6c" src="https://github.com/user-attachments/assets/5849245b-9c96-43c2-9df8-79e26cc221b2" />

# reflection about line y=x

<img width="638" height="476" alt="494296682-0b023dbe-eb9c-4779-a150-a07a93d20be0" src="https://github.com/user-attachments/assets/40cccecf-a2be-4315-af8a-e7492028c1f3" />


<img width="638" height="477" alt="494296726-7c4cce99-884f-4761-8538-e0ec6f609508" src="https://github.com/user-attachments/assets/a9df9bfd-ce4a-4be2-939e-e97df2061278" />

# reflection about line y=-x


<img width="642" height="476" alt="494296899-34b1ce93-94d7-41c2-a840-2f3d7c956821" src="https://github.com/user-attachments/assets/324b82b8-65d6-414d-820f-9994391cc231" />




<img width="633" height="473" alt="494296946-95ca0243-a708-4b9e-81d0-82849e8bf6ea" src="https://github.com/user-attachments/assets/5f71fc01-5437-4255-8af2-00fd67fb7b2e" />








# x shear with y reference line

<img width="638" height="476" alt="494318423-3cf0c5fb-3769-42df-9e33-b44f61968170" src="https://github.com/user-attachments/assets/094cbd6f-bb15-466d-b190-2fbd0004398e" />



<img width="635" height="472" alt="494318501-20d816c8-803c-4f58-9d0f-bddaaa8da7b4" src="https://github.com/user-attachments/assets/083a8a4d-b7e9-4b22-9f99-fc7ab6cbb947" />


# y shear with x reference line
<img width="641" height="473" alt="494318732-1f82d463-ced3-4bb3-91b0-b206a2ba4df9" src="https://github.com/user-attachments/assets/e5d85bc9-47b7-4186-a09c-0b3901cd7724" />



<img width="636" height="470" alt="494318826-39c39f5d-b966-4f1c-aed5-67c0cf1baa03" src="https://github.com/user-attachments/assets/f8da991f-72a9-4028-aeaa-653406880020" />










**Result :**
Thus, the program was Completed and the output was obtained successfully.
