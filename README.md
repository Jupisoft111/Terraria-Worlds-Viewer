# Terraria-Worlds-Viewer
Loads Terraria worlds as read-only and generates full world maps as images, it also displays world and blocks info

To generate a world map, you can also just navigate to your Terraria world files, usually at your documents folder, then "My Games", then "Terraria" and finally "Worlds", then just select the world you want and drag and drop it to this application window, then just wait a few seconds.

All the included source code files with a name that starts with "Terraria_" contain parts of the original source code of Terraria and are needed to be able to read the world files exactly as Terraria does. They were decompiled with ILSpy using the Terraria version 1.4.3.6, so right now it's up to date.

Also the code includes the colors of all the blocks (or tiles), and those were calculated with several functions designed by Jupisoft: first the original block textures were exported to PNG from the "Content" folder of Terraria itself thanks to the "XNA Extractor" by Jupisoft (also included in the "Minecraft Tools" by Jupisoft), and then the average color of each texture was calculated with the function "Obtener_Color_Medio_Imagen(), included in this source code".

For copyright reasons no original Terraria image or resource was included in this release, and the included code mentioned above was the minimum necessary to be able to properly read the world files.

Note: ILSpy returned some weird code, and I'm not sure if I translated it correctly. Here is the original returned code:

int num3 = (byte)((b3 & 0xC0) >> 6) switch
{
    0 => 0,
    1 => reader.ReadByte(),
    _ => reader.ReadInt16(),
};

I'm not sure if I ported this well or not, so here is what I've done:

int num3 = (byte)((b3 & 0xC0) >> 6);
if (num3 == 0) num3 = 0;
else if (num3 == 1) num3 = reader.ReadByte();
else num3 = reader.ReadInt16();

So far I haven't found any error while reading world files, but I can't totally say that there isn't any error.

The above code is located in the file "Terraria_WorldFile.cs", in the function "public static void LoadWorldTiles(BinaryReader reader, bool[] importance)".

Please let me know if I made any mistake by sending a mail to Jupitermauro@gmail.com or posting a comment to GitHub, thanks in advance.

Also after testing several world files, it seems that on the most left and right world borders (specially the left by what I've seen so far), there are misplaced blocks and even liquids, but in game I can't seem to travel to proper world ends, so perhaps those are bugs that the Terraria devs didn't find. So right now I'm not sure if I should report a possible bug in the world generation or not. Please let me know your thoughts about that.
