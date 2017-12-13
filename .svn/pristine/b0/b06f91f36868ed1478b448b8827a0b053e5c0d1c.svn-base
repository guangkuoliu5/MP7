/**
 * A class that runs implements several simple transformations on 2D image arrays.
 * <p>
 * This file contains stub code for your image transformation methods that are called by the main
 * class. You will do your work for this MP in this file.
 * <p>
 * Note that you can make several assumptions about the images passed to your functions, both by the
 * web front end and by our testing harness:
 * <ul>
 * <li>You will not be passed empty images.</li>
 * <li>All images will have even width and height.</li>
 * </ul>
 *
 * @see <a href="https://cs125.cs.illinois.edu/MP/4/">MP4 Documentation</a>
 */
import java.util.ArrayList;
import java.util.Random;
public class Transform {
    public static int steps = 0;
    public static boolean gs = false;
    public static ArrayList<Integer> hist = new ArrayList<Integer>();
    public static int[][] temp = new int[0][0];
    public static int N = 3;
    public static int level = 5;
    public static int[][] map = new int[N][N];
    public static int[][] answer = new int[N][N];
    public static boolean flag = false;
    /**
     * Default amount to shift an image's position. Not used by the testing suite, so feel free to
     * change this value.
     */
    public static final int DEFAULT_POSITION_SHIFT = 16;

    /**
     * Pixel value to use as filler when you don't have any valid data. All white with complete
     * transparency. DO NOT CHANGE THIS VALUE: the testing suite relies on it.
     */
    public static final int FILL_VALUE = 0xFFFFFFF;
    /**
     *  .
     * @param verti asdfsd
     * @param hori afsdfa
     * @return asfasf
     */
    public static int[][] paint(final int hori, final int verti) {
        int[][] ans = new int[hori][verti];
        for (int i = 0; i < hori; i++) {
            for (int j = 0; j < verti; j++) {
                ans[i][j] = FILL_VALUE;
            }
        }
        return ans;
    }

    public static int[][] produce(int[][] orgImage) {
        int hori = orgImage.length;
        int verti = orgImage[0].length;
        int[][] proImage = paint(hori, verti);
        hori = (int) (N * Math.floor(hori * 1.0/ N));
        verti = (int) (N * Math.floor(verti * 1.0 / N));
        for (int j = 0; j < N; j++) {
            for (int i = 0; i < N; i++) {
                if (map[j][i] != 0) {
                    int outi = i * hori / N;
                    int outj = j * verti / N;
                    int inj = (int) Math.ceil(map[j][i] * 1.0 / N) - 1;
                    int ini = map[j][i] - inj * N - 1;
                    ini = ini * hori / N;
                    inj = inj * verti / N;
                    for (int ph = 5; ph < hori / N; ph++) {
                        for (int pv = 5; pv < verti / N; pv++) {
                            proImage[outi + ph][outj + pv] = orgImage[ini + ph][inj + pv];
                        }
                    }
                }
            }
        }
        return proImage;
    }

    public static int[][] mystery(final int[][] originalImage) {
        hist.clear();
        gs = false;

        int[] a = new int[N * N];
        map = new int[N][N];
        answer = new int[N][N];
        for (int i = 0; i < N * N; i++) {
            a[i] = i;
        }
        for (int j = 0; j < N; j++) {
            for (int i = 0; i < N; i++) {
                if(i + j != 2 * N - 2) {
                    map[j][i] = a[j * N + i + 1];
                    answer[j][i] = a[j * N + i + 1];

                }
            }
        }
        map[N - 1][N - 1] = 0;
        answer[N - 1][N - 1] = 0;
        for (int i = 0; i < level; i++) {
            Random rand = new Random();
            switch (rand.nextInt(4)) {
                case 0:
                    shiftLeft(originalImage, 1);
                    if (!flag) {
                        i--;
                    }
                    break;
                case 1:
                    shiftRight(originalImage, 1);
                    if (!flag) {
                        i--;
                    }
                    break;
                case 2:
                    shiftUp(originalImage, 1);
                    if (!flag) {
                        i--;
                    }
                    break;
                case 3:
                    shiftDown(originalImage, 1);
                    if (!flag) {
                        i--;
                    }
                    break;
                default :
                    shiftLeft(originalImage, 1);
                    if (!flag) {
                        i--;
                    }
                    break;
            }

        }
        steps = 0;
        gs = true;
        System.out.println("----------------------------------------\nNew Game Started!\nCurrent Dimension: "
        + N + "\nCurrent Difficulty: " + level + "\nGood Luck!");
        return produce(originalImage);
    }
    public static int[][] moreRed(final int[][] originalImage, final int amount) {
        N++;
        return mystery(originalImage);
    }

    public static int[][] lessRed(final int[][] originalImage, final int amount) {
        N--;
        return mystery(originalImage);
    }
    public static int[][] moreGreen(final int[][] originalImage, final int amount) {
        level+=10;
        return mystery(originalImage);
    }

    public static int[][] lessGreen(final int[][] originalImage, final int amount) {
        if(level > 5)level-=10;
        return mystery(originalImage);
    }

    public static int[][] shiftLeft(final int[][] originalImage, final int amount) {
        int i0 = 0;
        int j0 = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[j][i] == 0) {
                    i0 = i;
                    j0 = j;
                    break;
                }
            }
            if (map[j0][i0] == 0) {
                break;
            }
        }
        flag = false;
        if (i0 < N - 1) {
            map[j0][i0] = map[j0][i0 + 1];
            map[j0][i0 + 1] = 0;
            hist.add(1);
            steps++;
            flag = true;
        }
        boolean won = true;
        for (int j = 0; j < N; j++) {
            for (int i = 0; i < N; i++) {
                if (map[i][j] != answer[i][j]) {
                    won = false;
                }
            }
        }

        if (won) {
            if(gs) {

                System.out.println("\n\nYou win!!!\nYou have made " + steps + " number of moves to win.");
            }
            return originalImage;
        }
        return produce(originalImage);
    }

    /*
     * Shift right like above.
     */
    /**
     * .
     * @param originalImage sadf
     * @param amount sadf
     * @return saf
     */
    public static int[][] shiftRight(final int[][] originalImage, final int amount) {
        int i0 = 0;
        int j0 = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[j][i] == 0) {
                    i0 = i;
                    j0 = j;
                    break;
                }
            }
            if (map[j0][i0] == 0) {
                break;
            }
        }
        flag = false;
        if (i0 > 0) {
            map[j0][i0] = map[j0][i0 - 1];
            map[j0][i0 - 1] = 0;
            hist.add(2);
            steps++;
            flag = true;
        }
        boolean won = true;
        for (int j = 0; j < N; j++) {
            for (int i = 0; i < N; i++) {
                if (map[i][j] != answer[i][j]) {
                    won = false;
                }
            }
        }
        if (won) {
            if(gs) {
                System.out.println("\n\nYou win!!!\nYou have made " + steps + " number of moves to win.");
            }
            return originalImage;
        }
        return produce(originalImage);
    }

    /**
     * Shift up like above.
     */
    /**
     * sg.
     * @param originalImage asdf
     * @param amount sadf
     * @return asdffad
     */
    public static int[][] shiftUp(final int[][] originalImage, final int amount) {
        int i0 = 0;
        int j0 = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[j][i] == 0) {
                    i0 = i;
                    j0 = j;
                    break;
                }
            }
            if (map[j0][i0] == 0) {
                break;
            }
        }
        flag = false;
        if (j0 < N - 1) {
            map[j0][i0] = map[j0 + 1][i0];
            map[j0 + 1][i0] = 0;
            hist.add(3);
            steps++;
            flag = true;
        }
        boolean won = true;
        for (int j = 0; j < N; j++) {
            for (int i = 0; i < N; i++) {
                if (map[i][j] != answer[i][j]) {
                    won = false;
                }
            }
        }
        if (won) {
            if(gs){

                System.out.println("\n\nYou win!!!\nYou have made " + steps + " number of moves to win.");

            }
            return originalImage;
        }
        return produce(originalImage);
    }

    /**
     * Shift down like above.
     */
    /**
     *  asdf.
     * @param originalImage sadf
     * @param amount adsf
     * @return safasf
     */
    public static int[][] shiftDown(final int[][] originalImage, final int amount) {
        int i0 = 0;
        int j0 = 0;
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (map[j][i] == 0) {
                    i0 = i;
                    j0 = j;
                    break;
                }
            }
            if (map[j0][i0] == 0) {
                break;
            }
        }
        flag = false;
        if (j0 > 0) {
            map[j0][i0] = map[j0 - 1][i0];
            map[j0 - 1][i0] = 0;
            hist.add(4);
            steps++;
            flag = true;
        }
        boolean won = true;
        for (int j = 0; j < N; j++) {
            for (int i = 0; i < N; i++) {
                if (map[i][j] != answer[i][j]) {
                    won = false;
                }
            }
        }
        if (won) {
            if (gs) {
                System.out.println("\n\nYou win!!!\nYou have made " + steps + " number of moves to win.");

            }
            return originalImage;
        }
        return produce(originalImage);
    }

    /**
     * Rotate the image left by 90 degrees around its center.
     * <p>
     * Any pixels rotated in from off screen should be filled with FILL_VALUE. This function <i>does
     * not modify the original image</i>.
     *
     * @param originalImage the image to rotate left 90 degrees
     * @return the rotated image
     */
    public static int[][] rotateLeft(final int[][] originalImage) {
        int sz = hist.size();
        if (sz == 0) {
            return produce(originalImage);
        }
        switch(hist.get(sz - 1)) {
            case 1:
                temp = shiftRight(originalImage, 1);
                hist.remove(hist.size() - 1);
                hist.remove(hist.size() - 1);
                return temp;
            case 2:
                temp = shiftLeft(originalImage, 1);
                hist.remove(hist.size() - 1);
                hist.remove(hist.size() - 1);
                return temp;
            case 3:
                temp = shiftDown(originalImage, 1);
                hist.remove(hist.size() - 1);
                hist.remove(hist.size() - 1);
                return temp;
            case 4:
                temp = shiftUp(originalImage, 1);
                hist.remove(hist.size() - 1);
                hist.remove(hist.size() - 1);
                return temp;
            default:
                break;
        }
        return produce(originalImage);

    }

    /*
     * Rotate the image right like above.
     */
    /**
     *  f.
     * @param originalImage dgfs
     * @return sadg
     */
    public static int[][] rotateRight(final int[][] originalImage) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        shiftImage = paint(hori, verti);
        double centerx = (hori - 1) * 1.0 / 2.0;
        double centery = (verti - 1) * 1.0 / 2.0;
        double shor = centerx;
        if (centerx > centery) {
            shor = centery;
        }
        for (int i = (int) (centerx - shor); i <= (int) (centerx + shor); i++) {
            for (int j = (int) (centery - shor); j <= (int) (centery + shor); j++) {
                double x = i - centerx;
                double y = centery - j;
                double x0 = -y;
                double y0 = x;
                int i0 = (int) (x0 + centerx);
                int j0 = (int) (centery - y0);
                shiftImage[i][j] = originalImage[i0][j0];
            }
        }
        return shiftImage;
    }

    /*
     * Flip the image on the vertical axis across its center.
     */
    /**
     * sadf.
     * @param originalImage sg
     * @return sdfg
     */
    public static int[][] flipVertical(final int[][] originalImage) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        for (int i = 0; i < hori; i++) {
            for (int j = 0; j < verti; j++) {
                shiftImage[i][j] = originalImage[i][verti - j - 1];
            }
        }
        return shiftImage;
    }

    /*
     * Flip the image on the horizontal axis across its center.
     */
    /**
     *  sadgg.
     * @param originalImage ghfj
     * @return dfgh
     */
    public static int[][] flipHorizontal(final int[][] originalImage) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        for (int i = 0; i < hori; i++) {
            for (int j = 0; j < verti; j++) {
                shiftImage[i][j] = originalImage[hori - 1 - i][j];
            }
        }
        return shiftImage;
    }

    /**
     * Default amount to shift colors by. Not used by the testing suite, so feel free to change this
     * value.
     */
    public static final int DEFAULT_COLOR_SHIFT = 32;
    /**
     * asdf.
     */
    public static final int COLORLEAP = 0x100;
    /**
     * asdf.
     */
    public static final int REDINDEX = 0;
    /**
     * asdf.
     */
    public static final int GREENINDEX = 8;
    /**
     * asdf.
     */
    public static final int BLUEINDEX = 2 * 8;
    /**
     * asdf.
     */
    public static final int ALPHAINDEX = 3 * 8;
    /**
     * asdf.
     */
    public static final int UPPER = 0xff;
    /**
     * asd f.
     * @param original jdfj
     * @param colorindex dh
     * @return ssdfggf
     */
    public static int extract(final int original, final int colorindex) {
        int ans = (original >>> colorindex) % COLORLEAP;
        if (ans < 0) {
            ans += COLORLEAP;
        }
        return ans;
    }
    /**
     * dsa f.
     * @param original sd fa
     * @param amount asdf
     * @param colorindex asdf
     * @return asdff
     */
    public static int coloradd(final int original, final int amount, final int colorindex) {
        int org = extract(original, colorindex);
        int added = org + amount;
        if (added >= UPPER) {
            added = UPPER;
        } else if (added <= 0) {
            added = 0;
        }
        int ans = original - (org << colorindex) + (added << colorindex);
        return ans;
    }
    /**
     *  asd f.
     * @param originalImage asdf d f
     * @param amount asff
     * @param colorindex asd f
     * @return  asdf
     */
    public static int[][] colorshift(final int[][] originalImage,
            final int amount, final int colorindex) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        for (int i = 0; i < hori; i++) {
            for (int j = 0; j < verti; j++) {
                shiftImage[i][j] = coloradd(originalImage[i][j], amount, colorindex);
            }
        }
        return shiftImage;
    }
    /**
     * Add red to the image.
     * <p>
     * This function <i>does not modify the original image</i>. It should also not generate any new
     * filled pixels.
     *
     * @param originalImage the image to add red to
     * @param amount the amount of red to add
     * @return the recolored image
     */


    /*
     * Add green to the image.
     */
    /**
     * d saf.
     * @param originalImage sadf
     * @param amount sa f
     * @return  sadfa
     */


    /*
     * Add blue to the image.
     */
    /**
     *  asdfasdf.
     * @param originalImage asasdf
     * @param amount sadfasf
     * @return sfdaf
     */
    public static int[][] moreBlue(final int[][] originalImage,
            final int amount) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        shiftImage = colorshift(originalImage, amount, BLUEINDEX);
        return shiftImage;
    }

    /*
     * Remove blue from the image.
     */
    /**
     * \.
     * @param originalImage sdaf
     * @param amount sda
     * @return asdf s
     */
    public static int[][] lessBlue(final int[][] originalImage, final int amount) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        shiftImage = colorshift(originalImage, -amount, BLUEINDEX);
        return shiftImage;
    }

    /*
     * Increase the image alpha channel.
     */
    /**
     * d saf .
     * @param originalImage dsaf
     * @param amount d saf
     * @return dsaf
     */
    public static int[][] moreAlpha(final int[][] originalImage, final int amount) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        shiftImage = colorshift(originalImage, amount, ALPHAINDEX);
        return shiftImage;
    }

    /*
     * Decrease the image alpha channel.
     */
     /**
      * asdf.
      * @param originalImage sadf
      * @param amount sdaf
      * @return sadf a
      */
    public static int[][] lessAlpha(final int[][] originalImage, final int amount) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        shiftImage = colorshift(originalImage, -amount, ALPHAINDEX);
        return shiftImage;
    }

    /**
     * The default resize factor. Not used by the testing suite, so feel free to change this value.
     */
    public static final int DEFAULT_RESIZE_AMOUNT = 2;

    /**
     * Shrink in the vertical axis around the image center.
     * <p>
     * An amount of 2 will result in an image that is half its original height. An amount of 3 will
     * result in an image that's a third of its original height. Any pixels shrunk in from off
     * screen should be filled with FILL_VALUE. This function <i>does not modify the original
     * image</i>.
     *
     * @param originalImage the image to shrink
     * @param amount the factor by which the image's height is reduced
     * @return the shrunken image
     */
    public static int[][] shrinkVertical(final int[][] originalImage, final int amount) {
        int verti = originalImage.length;
        int hori = originalImage[0].length;
        int[][] shiftImage = new int[verti][hori];
        return shiftImage;
    }

    /*
     * Expand in the vertical axis around the image center.
     */
    /**
     *
     *
    /**
     * das f.
     * @param originalImage asd
     * @param amount safd
     * @return asfd
     */
    public static int[][] expandVertical(final int[][] originalImage, final int amount) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        double centery = (verti - 1.0) / 2.0;
        for (int i = 0; i < hori; i++) {
            for (int j = 0; j < verti; j++) {
                double y = centery - j;
                double y0 = y / (1.0 * amount);
                int j0 = (int) Math.round(centery - y0);
                shiftImage[i][j] = originalImage[i][j0];
            }
        }
        return shiftImage;
    }

    /*
     * Shrink in the horizontal axis around the image center.
     */
    /**
     *  sadf.
     * @param originalImage sdaf
     * @param amount asdfzf
     * @return sd af
     */
    public static int[][] shrinkHorizontal(final int[][] originalImage, final int amount) {
        int verti = originalImage.length;
        int hori = originalImage[0].length;
        int[][] shiftImage = new int[verti][hori];
        return shiftImage;
    }

    /*
     * Expand in the horizontal axis around the image center.
     */
    /**
     *  sdfg.
     * @param originalImage af
     * @param amount asdf
     * @return asfd
     */
    public static int[][] expandHorizontal(final int[][] originalImage, final int amount) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        double centerx = (hori - 1.0) / 2.0;
        for (int i = 0; i < hori; i++) {
            for (int j = 0; j < verti; j++) {
                double x = i - centerx;
                double x0 = x / (1.0 * amount);
                int i0 = (int) Math.round(centerx + x0);
                shiftImage[i][j] = originalImage[i0][j];
            }
        }
        return shiftImage;
    }
    /**
     *  afd .
     */
    public static final int GUP = 200;
    /**
     * Remove a green screen mask from an image.
     * <p>
     * This function should remove primarily green pixels from an image and replace them with
     * transparent pixels (FILL_VALUE), allowing you to achieve a green screen effect. Obviously
     * this function will destroy pixels, but it <i>does not modify the original image</i>.
     * <p>
     * While this function is tested by the test suite, only extreme edge cases are used. Getting it
     * work work will with real green screen images is left as a challenge for you.
     *
     * @param originalImage the image to remove a green screen from
     * @return the image with the green screen removed
     */
    public static int[][] greenScreen(final int[][] originalImage) {
        int hori = originalImage.length;
        int verti = originalImage[0].length;
        int[][] shiftImage = new int[hori][verti];
        for (int i = 0; i < hori; i++) {
            for (int j = 0; j < verti; j++) {
                shiftImage[i][j] = originalImage[i][j];
                int org = extract(originalImage[i][j], GREENINDEX);
                if (org > GUP) {
                    shiftImage[i][j] = FILL_VALUE;
                }
            }
        }
        return shiftImage;
    }
}
