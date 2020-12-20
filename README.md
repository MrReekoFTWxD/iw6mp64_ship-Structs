# Ghosts MP Structs
- Steam Product Version 3.15

## SysInfo
```cpp
class sys_Info
{
public:
	double cpuGHz; //0x0000
	double configureGHz; //0x0008
	int32_t logicalCpuCount; //0x0010
	int32_t physicalCpuCount; //0x0014
	int32_t sysMB; //0x0018
	char gpuDescription[512]; //0x001C
	char pad_021C[12]; //0x021C
	bool SSE; //0x0228
	char cpuVendor[13]; //0x0229
	char cpuName[49]; //0x0236
}; //Size: 0x0267
```

## Material and Font

```cpp
union GFxDrawSurfFields
{
	unsigned long long unused;
	unsigned long long primarySortKey;
	unsigned long long surfType;
	unsigned long long primaryLightIndex;
	unsigned long long prepass;
	unsigned long long materialSortedIndex;
	unsigned long long customIndex;
	unsigned long long reflectionProbeIndex;
	unsigned long long objectId;
};
 
union GfxDrawSurf 
{
	GFxDrawSurfFields fields;
	unsigned long long packed;
};

struct MaterialInfo 
{
	const char *name;
	char gameFlags;
	char sortKey;
	char textureAtlasRowCount;
	char textureAtlasColumnCount;
	GfxDrawSurf drawSurf;
	int surfaceTypeBits;
	char unknown[0xC];
};

struct Material	
{
	MaterialInfo info; 
}; //CBA with this struct

struct Glyph
{
  unsigned __int16 letter;
  char x0;
  char y0;
  char dx;
  char pixelWidth;
  char pixelHeight;
  float s0;
  float t0;
  float s1;
  float t1;
};

struct Font 
{
    const char * name;
    int pixelHeight;
    int glyphCount;
    Material * material;
    Material * glowMaterial;
    Glyph * glyphs;
};
```
## UiContext
```cpp
enum class LocalClientNum_t : int32_t
{
	LOCAL_CLIENT_INVALID = -1,
	LOCAL_CLIENT_0 = 0x0,
	LOCAL_CLIENT_LAST = 0x0,
	LOCAL_CLIENT_COUNT = 0x1,
};

class cursorPos
{
public:
	float x; //0x0000
	float y; //0x0004
}; //Size: 0x0008

class UiContext
{
public:
	LocalClientNum_t localClientNum; //0x0000
	float bias; //0x0004
	int32_t realTime; //0x0008
	int32_t frameTime; //0x000C
	class cursorPos cursor; //0x0010
	int32_t inWindow; //0x0018
	int32_t isCursorVisible; //0x001C
	int32_t paintFull; //0x0020
	int32_t screenWidth; //0x0024
	int32_t screenHeight; //0x0028
	float screenAspect; //0x002C
	float FPS; //0x0030
}; //Size: 0x0034
```
## cgArray

```cpp
enum statIndex_t
{
	STAT_HEALTH = 0x0,
	STAT_DEAD_YAW = 0x1,
	STAT_MAX_HEALTH = 0x2,
	STAT_SPAWN_COUNT = 0x3,
	MAX_STATS = 0x4,
};

enum class ViewLockTypes : int32_t
{
	PLAYERVIEWLOCK_NONE = 0x0,
	PLAYERVIEWLOCK_FULL = 0x1,
	PLAYERVIEWLOCK_WEAPONJITTER = 0x2,
	PLAYERVIEWLOCKCOUNT = 0x3,
};

enum class KillCamEntityType : int32_t
{
	KC_NO_ENTITY = 0x0,
	KC_HELICOPTER = 0x1,
	KC_AIRSTRIKE = 0x2,
	KC_EXPLOSIVE = 0x3,
	KC_FAST_EXPLOSIVE = 0x4,
	KC_ROCKET = 0x5,
	KC_ROCKET_CORPSE = 0x6,
	KC_TURRET = 0x7,
	KC_JAVELIN = 0x8,
	KC_REMOTE_MISSILE = 0x9,
};

enum class KillCamEntityRestState : int32_t
{
	KC_ENT_MOVING = 0x0,
	KC_ENT_AT_REST = 0x1,
	KC_ENT_STUCK_GROUND = 0x2,
	KC_ENT_STUCK_WALL = 0x3,
	KC_ENT_STUCK_PERSON = 0x4,
};

enum class team_t : int32_t
{
	TEAM_FREE = 0x0,
	TEAM_BAD = 0x0,
	TEAM_AXIS = 0x1,
	TEAM_ALLIES = 0x2,
	TEAM_SPECTATOR = 0x3,
	TEAM_NUM_TEAMS = 0x4,
};

class PlayerVehicleState
{
public:
	int32_t entity; //0x0000
	int32_t flags; //0x0004
	int32_t targetEntity; //0x0008
	vec3_t origin; //0x000C
	vec3_t angles; //0x0018
	vec3_t velocity; //0x0024
	vec3_t angVelocity; //0x0030
	vec2_t tilt; //0x003C
	vec2_t tiltVelocity; //0x0044
	vec2_t gunAngles; //0x004C
	uint32_t splineId; //0x0054
	uint32_t splineNodeIndex; //0x0058
	float splineLambda; //0x005C
	float corridorSpeeds[2]; //0x0060
}; //Size: 0x0068

class EntityEvent
{
public:
	int32_t eventType; //0x0000
	int32_t eventParm; //0x0004
}; //Size: 0x0008

class playerEvents_t
{
public:
	int32_t eventSequence; //0x0000
	class EntityEvent events[4]; //0x0004
	int32_t oldEventSequence; //0x0024
	int32_t timeADSCameUp; //0x0028
}; //Size: 0x002C

class SprintState_s
{
public:
	int32_t sprintButtonUpRequired; //0x0000
	int32_t sprintDelay; //0x0004
	int32_t lastSprintStart; //0x0008
	int32_t lastSprintEnd; //0x000C
	int32_t sprintStartMaxLength; //0x0010
}; //Size: 0x0014

class compressedAnimData_s
{
public:
	int32_t flags; //0x0000
	int32_t animRate; //0x0004
	int32_t distanceIn2D; //0x0008
	int32_t distanceOut2D; //0x000C
	int32_t distanceInZ; //0x0010
	int32_t distanceOutZ; //0x0014
	int32_t endScriptAnimTableIndex; //0x0018
}; //Size: 0x001C

class MantleState
{
public:
	float yaw; //0x0000
	int32_t startPitch; //0x0004
	int32_t transIndex; //0x0008
	int32_t flags; //0x000C
	int32_t startTime; //0x0010
	vec3_t startPosition; //0x0014
	class compressedAnimData_s compressedAnimData; //0x0020
}; //Size: 0x003C

class SlideState
{
public:
	int32_t flags; //0x0000
	int32_t noFricTime; //0x0004
}; //Size: 0x0008

class PlayerActiveWeaponState
{
public:
	int32_t weapAnim; //0x0000
	int32_t weaponTime; //0x0004
	int32_t weaponDelay; //0x0008
	int32_t weaponRestrictKickTime; //0x000C
	int32_t weaponState; //0x0010
	int32_t weapHandFlags; //0x0014
	uint32_t weaponShotCount; //0x0018
}; //Size: 0x001C

class Weapon
{
public:
	int32_t __03; //0x0000
	int32_t data; //0x0004
}; //Size: 0x0008

class PlayerEquippedWeaponState
{
public:
	bool usedBefore; //0x0000
	bool dualWielding; //0x0001
	bool inAltMode; //0x0002
	bool needsRechamber[2]; //0x0003
	char pad_0005[3]; //0x0005
	int32_t zoomLevelIndex; //0x0008
	bool thermalEnabled; //0x000C
	bool hybridScope; //0x000D
	char pad_000E[2]; //0x000E
}; //Size: 0x0010

class playerState_s
{
public:
	int32_t commandTime; //0x0000
	int32_t pm_type; //0x0004
	int32_t pm_time; //0x0008
	int32_t pm_flags; //0x000C
	int32_t otherFlags; //0x0010
	int32_t linkFlags; //0x0014
	int32_t bobCycle; //0x0018
	vec3_t origin; //0x001C
	vec3_t velocity; //0x0028
	int32_t grenadeTimeLeft; //0x0034
	int32_t throwbackGrenadeOwner; //0x0038
	int32_t throwbackGrenadeTimeLeft; //0x003C
	int32_t throwbackWeapon; //0x0040
	int32_t movingPlatformEntity; //0x0044
	int32_t remoteEyesEnt; //0x0048
	int32_t remoteEyesTagname; //0x004C
	int32_t remoteControlEnt; //0x0050
	int32_t remoteTurretEnt; //0x0054
	int32_t foliageSoundTime; //0x0058
	int32_t gravity; //0x005C
	int32_t speed; //0x0060
	vec3_t delta_angles; //0x0064
	int32_t groundEntityNum; //0x0070
	vec3_t vLadderVec; //0x0074
	int32_t jumpTime; //0x0080
	float jumpOriginZ; //0x0084
	int32_t legsTimer; //0x0088
	int32_t legsAnim; //0x008C
	int32_t torsoTimer; //0x0090
	int32_t torsoAnim; //0x0094
	int32_t animMoveType; //0x0098
	int32_t damageTimer; //0x009C
	int32_t damageDuration; //0x00A0
	int32_t flinch; //0x00A4
	int32_t movementDir; //0x00A8
	int32_t turnStartTime; //0x00AC
	int32_t turnDirection; //0x00B0
	int32_t turnRemaining; //0x00B4
	int32_t corpseIndex; //0x00B8
	class PlayerVehicleState vehicleState; //0x00BC
	int32_t eFlags; //0x0124
	class playerEvents_t pe; //0x0128
	int32_t unpredictableEventSequence; //0x0154
	int32_t unpredictableEventSequenceOld; //0x0158
	class EntityEvent unpredictableEvents[4]; //0x015C
	int32_t clientNum; //0x017C
	int32_t viewmodelIndex; //0x0180
	vec3_t viewangles; //0x0184
	int32_t viewHeightTarget; //0x0190
	float viewHeightCurrent; //0x0194
	int32_t viewHeightLerpTime; //0x0198
	int32_t viewHeightLerpTarget; //0x019C
	int32_t viewHeightLerpDown; //0x01A0
	vec2_t viewAngleClampBase; //0x01A4
	vec2_t viewAngleClampRange; //0x01AC
	int32_t damageEvent; //0x01B4
	int32_t damageYaw; //0x01B8
	int32_t damagePitch; //0x01BC
	int32_t damageCount; //0x01C0
	int32_t damageFlags; //0x01C4
	int32_t stats[4]; //0x01C8
	float proneDirection; //0x01D8
	float proneDirectionPitch; //0x01DC
	float proneTorsoPitch; //0x01E0
	ViewLockTypes viewlocked; //0x01E4
	int32_t viewlocked_entNum; //0x01E8
	vec3_t linkAngles; //0x01EC
	vec3_t linkWeaponAngles; //0x01F8
	int32_t linkWeaponEnt; //0x0204
	int32_t loopSound; //0x0208
	int32_t groundRefEnt; //0x020C
	int32_t cursorHint; //0x0210
	uint32_t cursorHintString; //0x0214
	int32_t cursorHintEntIndex; //0x0218
	int32_t cursorHintDualWield; //0x021C
	int32_t iCompassPlayerInfo; //0x0220
	int32_t radarEnabled; //0x0224
	int32_t radarBlocked; //0x0228
	int32_t radarMode; //0x022C
	int32_t radarStrength; //0x0230
	int32_t radarShowEnemyDirection; //0x0234
	int32_t sightedEnemyPlayersMask; //0x0238
	int32_t locationSelectionInfo; //0x023C
	class SprintState_s sprintState; //0x0240
	float holdBreathScale; //0x0254
	int32_t holdBreathTimer; //0x0258
	float moveSpeedScaleMultiplier; //0x025C
	float grenadeCookScale; //0x0260
	class MantleState mantleState; //0x0264
	class SlideState slideState; //0x02A0
	float leanf; //0x02A8
	class PlayerActiveWeaponState weapState[2]; //0x02AC
	class Weapon weaponsEquipped[15]; //0x02E4
	class PlayerEquippedWeaponState weapEquippedData[12]; //0x035C
	int32_t weapon; //0x041C
	char pad_0420[4]; //0x0420
	float FovScale; //0x0424
	float weaponSpread; //0x0428
	char pad_042C[252]; //0x042C
	int32_t lethal; //0x0528
	char pad_052C[12]; //0x052C
	int32_t tactical; //0x0538
	char pad_053C[12]; //0x053C
	int32_t primaryClip; //0x0548
	char pad_054C[12]; //0x054C
	int32_t secondaryClip; //0x0558
	char pad_055C[216]; //0x055C
	int32_t deltaTime; //0x0634
	char pad_0638[463440]; //0x0638
}; //Size: 0x71888

class GfxViewport
{
public:
	int32_t x; //0x0000
	int32_t y; //0x0004
	int32_t width; //0x0008
	int32_t height; //0x000C
}; //Size: 0x0010

class RefdefView
{
public:
	float tanHalfFovX; //0x0000
	float tanHalfFovY; //0x0004
	vec3_t org; //0x0008
	vec3_t axis[3]; //0x0014
	float zNear; //0x0038
}; //Size: 0x003C

class GfxDepthOfField
{
public:
	float viewModelStart; //0x0000
	float viewModelEnd; //0x0004
	float nearStart; //0x0008
	float nearEnd; //0x000C
	float farStart; //0x0010
	float farEnd; //0x0014
	float nearBlur; //0x0018
	float farBlur; //0x001C
}; //Size: 0x0020

class GfxFilm
{
public:
	bool enabled; //0x0000
	char pad_0001[3]; //0x0001
	float brightness; //0x0004
	float contrast; //0x0008
	float desaturation; //0x000C
	float desaturationDark; //0x0010
	bool invert; //0x0014
	char pad_0015[3]; //0x0015
	vec3_t tintDark; //0x0018
	vec3_t tintMedium; //0x0024
	vec3_t tintLight; //0x0030
}; //Size: 0x003C

class GfxMaterialBloom
{
public:
	float radius; //0x0000
	float pinch; //0x0004
	float intensity; //0x0008
	float luminanceCutoff; //0x000C
	float desaturation; //0x0010
}; //Size: 0x0014

class GfxMaterialBloomHQ
{
public:
	bool enable; //0x0000
	char pad_0001[3]; //0x0001
	float haziness; //0x0004
	float gamma; //0x0008
	float desaturation; //0x000C
}; //Size: 0x0010

class GfxLightScale
{
public:
	float diffuseScale; //0x0000
	float specularScale; //0x0004
}; //Size: 0x0008

class GfxCompositeFx 
{
public:
	GfxFilm film; //0x0000
	vec3_t distortionScale; //0x003C
	float blurRadius; //0x0048
	float distortionMagnitude; //0x004C
	float frameRate; //0x0050
	int32_t lastUpdate; //0x0054
	int32_t frame; //0x0058
	int32_t startMSec; //0x005C
	int32_t currentTime; //0x0060
	int32_t duration; //0x0064
	bool enabled; //0x0068
	bool scriptEnabled; //0x0069
	char pad_006A[2]; //0x006A
}; //Size: 0x006C

class refdef_t
{
public:
	GfxViewport displayPort;
	class RefdefView view; //0x0010
	vec3_t viewOffset; //0x004C
	vec3_t viewOffsetPrev; //0x0058
	int32_t time; //0x0064
	int32_t frameTime; //0x0068
	bool daltonize; //0x006C
	char pad_006D[3]; //0x006D
	float blurRadius; //0x0070
	char pad_0074[8]; //0x0074
	class GfxDepthOfField dof; //0x007C
	class GfxFilm film; //0x009C
	class GfxMaterialBloom materialBloom; //0x00D8
	class GfxMaterialBloomHQ materialBloomHQ; //0x00EC
	class GfxLightScale charPrimaryLightScale; //0x00FC
	class GfxLightScale viewModelPrimaryLightScale; //0x0104
	vec3_t charAmbience; //0x010C
	vec3_t viewModelAmbience; //0x0118
	class GfxCompositeFx waterSheetingFx; //0x0124
	float ssrFade; //0x0190
	class GfxViewport ssrSourceDisplayViewport; //0x0194
	char pad_01A4[36]; //0x01A4
}; //Size: 0x01C8

class PlayerDiveView
{
public:
	float diveYaw; //0x0000
	float roll; //0x0004
}; //Size: 0x0008

class characterInfo_t
{
public:
	int32_t entityNum; //0x0000
	int32_t infoValid; //0x0004
	int32_t nextValid; //0x0008
	team_t team; //0x000C
	team_t oldteam; //0x0010
	uint32_t perks[2]; //0x0014
	char model[64]; //0x001C
	char attachModelNames[6][64]; //0x005C
	char attachTagNames[6][64]; //0x01DC
	uint32_t partBits[6]; //0x035C
	int32_t leftHandGun; //0x0374
	int32_t dobjDirty; //0x0378
	char pad_037C[8]; //0x037C
	int32_t weapon; //0x0384
	char pad_0388[424]; //0x0388
	int32_t isShooting; //0x0530
	char pad_0534[4]; //0x0534
	int32_t isAds; //0x0538
	char pad_053C[156]; //0x053C
}; //Size: 0x05D8

class clientInfo_t
{
public:
	int32_t clientNum; //0x0000
	char name[16]; //0x0004
	int32_t rank_mp; //0x0014
	int32_t prestige_mp; //0x0018
	int32_t rank_alien; //0x001C
	int32_t prestige_alien; //0x0020
	char clanAbbrev[8]; //0x0024
	int32_t location; //0x002C
	int32_t health; //0x0030
	uint32_t playerCardPatch; //0x0034
	uint32_t playerCardBackground; //0x0038
	int8_t isMLGSpectator; //0x003C
	char pad_003D[15]; //0x003D
	uint32_t modelIndex[3]; //0x004C
	char pad_0058[8]; //0x0058
	Material* rankIconHandle; //0x0060
	char *rankDisplayLevel; //0x0068 
}; //Size: 0x0070


class snapShot_t
{
public:
	int32_t serverTime; //0x0000
	int32_t snapFlags; //0x0004
	int32_t ping; //0x0008
	char pad_000C[4]; //0x000C
	int32_t numEntities; //0x0010
	int32_t numClients; //0x0014
	char pad_0018[68]; //0x0018
	char mapFile[64]; //0x005C
}; //Size: 0x009C

class cg_t
{
public:
	playerState_s ps; //0x0000
	float frameInterpolation; //0x71888
	int32_t frameTime; //0x7188C
	int32_t time; //0x71890
	int32_t oldTime; //0x71894
	int32_t physicsTime; //0x71898
	int32_t groundEntityTime; //0x7189C
	uint32_t lastGroundSurfaceType; //0x718A0
	int32_t mapRestart; //0x718A4
	int32_t spectatingThirdPerson; //0x718A8
	int32_t renderingThirdPerson; //0x718AC
	float landChange; //0x718B0
	int32_t landTime; //0x718B4
	int32_t lastMantleflags; //0x718B8
	int32_t lastProneCrawlInputTime; //0x718BC
	char pad_718C0[8]; //0x718C0
	class refdef_t refdef; //0x718C8
	char pad_71A90[276548]; //0x71A90
	float compassNorthYaw; //0xB52D4
	vec2_t compassNorth; //0xB52D8
	Material *compassMapMaterial; //0xB52E0
	vec2_t compassMapUpperLeft; //0xB52E8
	vec2_t compassMapWorldSize; //0xB52F0
	int32_t compassFadeTime; //0xB52F8
	int32_t healthFadeTime; //0xB52FC
	int32_t ammoFadeTime; //0xB5300
	int32_t sprintFadeTime; //0xB5304
	int32_t offhandFadeTime; //0xB5308
	int32_t offhandFlashTime; //0xB530C
	char pad_B5310[56]; //0xB5310
	int32_t holdBreathTime; //0xB5348
	int32_t holdBreathInTime; //0xB534C
	int32_t holdBreathDelay; //0xB5350
	float holdBreathFrac; //0xB5354
	char pad_B5358[4]; //0xB5358
	class PlayerDiveView diveView; //0xB535C
	float radarProgress; //0xB5364
	vec2_t selectedLocation; //0xB5368
	float selectedLocationAngle; //0xB5370
	char pad_B5374[8]; //0xB5374
	int32_t isKillCam; //0xB537C
	int32_t killCamStartTime; //0xB5380
	int32_t killCamEndTime; //0xB5384
	bool killCamFirstFrameRan; //0xB5388
	char pad_B5389[3]; //0xB5389
	int32_t killCamEntity; //0xB538C
	int32_t invalidKillCamEntity; //0xB5390
	KillCamEntityType killCamEntityType; //0xB5394
	int32_t killCamLastEntityNum; //0xB5398
	vec3_t killCamLastEntityOrg; //0xB539C
	vec3_t killCamLastEntityAngles; //0xB53A8
	KillCamEntityRestState killCamEntityRestState; //0xB53B4
	int32_t killCamLookAtEntity; //0xB53B8
	vec3_t killCamLookAt; //0xB53BC
	vec3_t killCamHelicopterOffset; //0xB53C8
	int32_t killCamStoppedTime; //0xB53D4
	float killCamStoppedDecelTime; //0xB53D8
	vec3_t killCamStoppedPos; //0xB53DC
	vec3_t killCamStoppedVel; //0xB53E8
	vec3_t killCamPrevBombOrigin; //0xB53F4
	int32_t killCamLerpEndTime; //0xB5400
	vec3_t killCamOldViewAngles; //0xB5404
	vec3_t killCamOldViewOrg; //0xB5410
	char pad_B541C[285340]; //0xB541C
	class characterInfo_t characterInfo[18]; //0xFAEB8
	char pad_1017E8[35904]; //0x1017E8
	class clientInfo_t ci[18]; //0x10A428 - 10AC08
	char pad_10AC08[0x16B8F0]; //0x10AC08
	class snapShot_t snap;
}; //Size: 0x10C42E

```

## cg_entitiesArray
```cpp
enum class entityType : int8_t
{
	ET_GENERAL,
	ET_PLAYER,
	ET_PLAYER_CORPSE,
	ET_ITEM,
	ET_MISSILE,
	ET_INVISIBLE,
	ET_SCRIPTMOVER,
	ET_SOUND_BLEND,
	ET_FX,
	ET_LOOP_FX,
	ET_PRIMARY_LIGHT,
	ET_TURRET,
	ET_HELICOPTER,
	ET_PLANE,
	ET_VEHICLE,
	ET_VEHICLE_COLLMAP,
	ET_VEHICLE_CORPSE,
	ET_VEHICLE_SPAWNER,
	ET_AGENT,
	ET_AGENT_CORPSE
};

enum class trType_t : int32_t
{
	TR_STATIONARY = 0x0,
	TR_INTERPOLATE = 0x1,
	TR_LINEAR = 0x2,
	TR_LINEAR_STOP = 0x3,
	TR_SINE = 0x4,
	TR_GRAVITY = 0x5,
	TR_LOW_GRAVITY = 0x6,
	TR_ACCELERATE = 0x7,
	TR_DECELERATE = 0x8,
	TR_PHYSICS = 0x9,
	TR_ANIMATED_MOVER = 0xA,
	TR_FIRST_RAGDOLL = 0xB,
	TR_RAGDOLL = 0xB,
	TR_RAGDOLL_GRAVITY = 0xC,
	TR_RAGDOLL_INTERPOLATE = 0xD,
	TR_LAST_RAGDOLL = 0xD,
	NUM_TRTYPES = 0xE,
};

class GfxSkinCacheEntry
{
public:
	uint32_t frameCount; //0x0000
	int32_t skinnedCachedOffset; //0x0004
	uint16_t numSkinnedVerts; //0x0008
	char pad_000A[2]; //0x000A
}; //Size: 0x000C

class cpose_t
{
public:
	uint16_t lightingHandle; //0x0000
	entityType eType; //0x0002
	int8_t cullIn; //0x0003
	int8_t isRagdoll; //0x0004
	char pad_0005[3]; //0x0005
	int32_t ragdollHandle; //0x0008
	int32_t killcamRagdollHandle; //0x000C
	int64_t physObjId; //0x0010
	vec3_t origin; //0x0018
	vec3_t angles; //0x0024
	vec3_t prevOrigin; //0x0030
	vec3_t prevAngles; //0x003C
	class GfxSkinCacheEntry skinCacheEntry; //0x0048
	char pad_0054[60]; //0x0054
}; //Size: 0x0090

class trajectory_t
{
public:
	trType_t trType; //0x0000
	int32_t trTime; //0x0004
	int32_t trDuration; //0x0008
	vec3_t trBase; //0x000C
	vec3_t trDelta; //0x0018
}; //Size: 0x0024

class LerpEntityState
{
public:
	int32_t eFlags; //0x0000
	class trajectory_t pos; //0x0004
	class trajectory_t apos; //0x0028
}; //Size: 0x004C

class entityState_t
{
public:
	int32_t number; //0x0000
	int32_t eType; //0x0004
	class LerpEntityState lerp; //0x0008
	char pad_0054[36]; //0x0054
	int32_t otherEntityNum; //0x0078
	int32_t attackerEntityNum; //0x007C
	int32_t groundEntityNum; //0x0080
	char pad_0084[4]; //0x0084
	int32_t surfType; //0x0088
	char pad_008C[16]; //0x008C
}; //Size: 0x0054

class centity_s
{
public:
	cpose_t pose;
	class LerpEntityState prevState; //0x0090
	char pad_00DC[28]; //0x00DC
	class entityState_t nextState; //0x00F8
	char pad_0194[40]; //0x0194
	int32_t weapon; //0x01BC
	int32_t iInAltWeaponMode;
	char pad_01C0[60]; //0x01C0
	int32_t eFlags; //0x0200
	char pad_0204[52]; //0x0204

}; //Size: 0x0238
```

## ClientActive
```cpp
class usercmd_s
{
public:
	int32_t serverTime; //0x0000
	uint32_t buttons; //0x0004
	int32_t angles[3]; //0x0008
	int32_t weapon; //0x0014
	int32_t offhand; //0x0018
	int8_t forwardmove; //0x001C
	int8_t rightmove; //0x001D
	char pad_001E[30]; //0x001E
}; //Size: 0x003C

class ClientArchiveData
{
public:
	int32_t serverTime; //0x0000
	vec3_t origin; //0x0004
	vec3_t velocity; //0x0010
	int32_t bobCycle; //0x001C
	int32_t movementDir; //0x0020
	class PlayerVehicleState playerVehStateClientArchive; //0x0024
}; //Size: 0x008C

class outPacket_t
{
public:
	int32_t p_cmdNumber; //0x0000
	int32_t p_serverTime; //0x0004
	int32_t p_realtime; //0x0008
}; //Size: 0x000C

class clientActive_t
{
public:
	int32_t cgamePredictedDataServerTime; //0x0000
	vec3_t clViewangles; //0x0004
	char pad_0010[12]; //0x0010
	class usercmd_s cmds[128]; //0x001C
	int32_t cmdNumber; //0x1E1C
	class ClientArchiveData N00020DD9[256]; //0x1E20
	int32_t clientArchiveIndex; //0xAA20
	int32_t packetBackupCount; //0xAA24
	int32_t packetBackupMask; //0xAA28
	int32_t parseEntitiesCount; //0xAA2C
	int32_t parseClientsCount; //0xAA30
	int32_t parseOmnvarsCount; //0xAA34
	class outPacket_t outPackets[16]; //0xAA38
	char pad_AAF8[211620]; //0xAAF8


	usercmd_s *UserCmd(int number)
	{
		return &cmds[number & 0x7F];
	}
}; //Size: 0x3E59C
```
