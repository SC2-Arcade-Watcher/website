<template>
    <div class="profile-item">
        <router-link
            :to="{ name: 'profile_summary', params: {
                regionId: profile.regionId,
                realmId: profile.realmId,
                profileId: profile.profileId
            }}"
            class="player-link"
        >
            <v-list-item-avatar
                tile
            >
                <v-img v-if="profile.avatar" :src="$starc.profileAvatarUrl(profile.avatar)" class="avatar-img" cover/>
                <v-avatar
                    v-else
                    class="blank-avatar"
                    color="grey darken-3"
                    tile
                >
                    <v-icon dark>
                        mdi-account-question
                    </v-icon>
                </v-avatar>
            </v-list-item-avatar>
            <span v-if="profile.name" v-html="profile.name"/>
            <span v-else v-html="`${$starc.profileHandle(author)}`"/>
            <small v-if="showDiscriminator && profile.discriminator" v-html="`#${profile.discriminator}`" class="grey--text"></small>
        </router-link>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import * as starc from '@/starc-api/starc';

@Component
export default class ProfileItem extends Vue {
    @Prop({
        required: true,
    })
    readonly profile!: starc.ProfileBase;

    @Prop({
        default: false,
    })
    readonly showDiscriminator!: boolean;

    private get regionCode() {
        return starc.GameRegion[this.profile.regionId];
    }

    created() {
    }
}
</script>
