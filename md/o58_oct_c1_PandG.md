# Pacman and Ghost

กรณีที่ไม่มีผีตัวใดที่สามารถเดินไปหา Pacman ได้เลย เราจะชนะเสมอ

กำหนดให้ $ghost(x,y)$ เป็นเวลาที่น้อยที่สุดที่เป็นไปได้ที่จะมีผีอยู่ในตำแหน่ง $(x,y)$ ถ้าผีไม่สามารถเดินไปถึงได้ จะให้มีค่าเป็น $\infty$ ตารางนี้สามารถคำนวณได้ด้วยอัลกอริธึม Multiple Source Shortest Path ทั่วไป เช่น Dijkstra's หรือ BFS ก็ได้ในกรณีนี้

กำหนดให้ $pacman(x,y)$ เป็นเวลาน้อยที่สุดที่เป็นไปได้ที่ pacman จะเดินไปที่ช่อง $(x,y)$ 

เนื่องจาก Pacman จะสามารถเดินไปที่ตำแหน่ง $(x,y)$ ได้ก็ต่อเมื่อมันสามารถเดินไปในเวลาที่น้อยกว่าผีเท่านั้น เราจึงต้องพิจารณาด้วยว่า **$pacman(x,y)$ จะต้องมีค่าน้อยกว่า $ghost(x,y)$ เสมอ** ไม่เช่นนั้นเราจะกำหนดให้ $pacman(x,y)$ มีค่าเป็น $\infty$

เราจะชนะก็ต่อเมื่อมีคู่อันดับ $(x,y)$ ใดๆที่มีค่าเท่ากับ $T$

Time-complexity: $\mathcal{O}(R*C)$

> ตัวอย่างโค้ดคำนวณตาราง $pacman(x,y)$
```cpp
while(!q.empty()) {
  int x, y;
  auto[x, y] = q.front(); q.pop();
    
  for(int d = 0; d < 4; d++) {
    int xx = x + dx[d], yy = y + dy[d];
    if(!valid(xx,yy)) continue;
    
    if(pacman[xx][yy] == inf && pacman[x][y] + 1 < ghost[xx][yy]) {
      pacman[xx][yy] = pacman[x][y] + 1;
      q.push({xx, yy});
    }
  }
}
```
