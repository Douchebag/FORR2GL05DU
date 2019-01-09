# Verkefni 1
1. Game loop er lykkja sem keyrir stanslaust á meðan leikur er í gang. Hvert skipti sem lykkjan er keyrð þarf hún að process-a user input, uppfæra stöðu leiksins og render-a leikinn. Lykkjan þarf að halda utan um tímann til að stjórna rate-inu af gameplay-inu og lykkjan þarf að keyra leikinn á stöðugum hraða þrátt fyrir mismun í vélbúnaði.
2. Leikjavél er framework fyrir leikjaþróun sem styður nokkra nauðsynlega hluti. Þú getur import-að teikningum og hönnunum, 2D og 3D frá öðrum hugbúnaði s.s. Photoshop og bætt þeim í senur og umhverfi. Þú getur líka bætt við lýsingu, hljóði, special effects, physics og animation, gagnvirkni, og gameplay logic-i. Þú getur líka edit-að, debug-að og optimize-að content-ið fyrir platform-in sem þú ert að miða fyrir. Unity styður upp að 25 platform-um í cross platform integration feature-inu þeirra á meðan Unreal Engine styður bara 10 platform. Unity er með mjög stórt community sem þú getur leitað þér hjálp til, styður margskonar file formats sem notuð er í stærstu 3d forritum og þú hefur aðgang að 15.000 fríum eða borguðum 3D models, hljóðum, animations, editor extensions, materials, script-um og shaders. Unity notar C# eða Javascript en UE notar C++. Ef þú notar UE þarft þú að borga 5% af öllum pening sem þú græðir af leiknum til Epic Games.
3. Til að líkja eftir hegðun hluta á raunverulegan hátt þarf að check-a hvort hlutirnir fari í árekstur við hvort annað í hvert skipti sem hlutirnir hreyfast og ef þeir snertast þá þurfum við að gera eitthvað í því s.s. að beita afli/krafti sem breytir hraða þeirra svo þeir færast í öfuga átt. 

Axis-aligned bounding boxes (AABB)
Fáum einskonar kassa utan um hlutinn okkar með þessu, þar sem min er vinstri neðra hornið og max er hægra efra hornið.
```C
typedef struct {
    float x;
    float y;
} Vector2;

typedef struct {
    Vector2 min;
    Vector2 max;
} AABB;
```
Til að testa hvort tveir AABB lenda í árekstri:
Ef einhver af gildunum er hærri en 0 þá eru hlutirnir ekki í árekstri.
```C
BOOL TestAABBOverlap(AABB* a, AABB* b)
{
    float d1x = b->min.x - a->max.x;
    float d1y = b->min.y - a->max.y;
    float d2x = a->min.x - b->max.x;
    float d2y = a->min.y - b->max.y;

    if (d1x > 0.0f || d1y > 0.0f)
        return FALSE;

    if (d2x > 0.0f || d2y > 0.0f)
        return FALSE;

    return TRUE;
}
```

