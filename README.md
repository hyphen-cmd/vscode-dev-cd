import pygame
import random

# 초기화
pygame.init()

# 화면 설정
WIDTH, HEIGHT = 600, 400
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("두더지 게임")

# 색깔
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
BROWN = (150, 75, 0)
RED = (255, 0, 0)

# 폰트 설정
font = pygame.font.Font(None, 36)

# 두더지 변수
mole_size = 50
mole_x = random.randint(50, WIDTH - 50)
mole_y = random.randint(50, HEIGHT - 50)
mole_appear_time = pygame.time.get_ticks()  # 두더지가 나타난 시간
mole_lifetime = 1000  # 두더지가 유지되는 시간 (1초)

# 점수
score = 0

# 게임 루프
running = True
while running:
    screen.fill(WHITE)  # 배경 흰색

    # 이벤트 처리
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.MOUSEBUTTONDOWN:
            mouse_x, mouse_y = event.pos
            # 두더지를 클릭했는지 확인
            if (mole_x - mole_size < mouse_x < mole_x + mole_size) and (mole_y - mole_size < mouse_y < mole_y + mole_size):
                score += 1
                mole_x = random.randint(50, WIDTH - 50)
                mole_y = random.randint(50, HEIGHT - 50)
                mole_appear_time = pygame.time.get_ticks()

    # 일정 시간이 지나면 두더지 위치 변경
    if pygame.time.get_ticks() - mole_appear_time > mole_lifetime:
        mole_x = random.randint(50, WIDTH - 50)
        mole_y = random.randint(50, HEIGHT - 50)
        mole_appear_time = pygame.time.get_ticks()

    # 두더지 그리기
    pygame.draw.circle(screen, BROWN, (mole_x, mole_y), mole_size)

    # 점수 표시
    score_text = font.render(f"Score: {score}", True, BLACK)
    screen.blit(score_text, (10, 10))

    pygame.display.flip()  # 화면 업데이트
    pygame.time.delay(50)  # 속도 조절

pygame.quit() 